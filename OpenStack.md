OpenStack
=====
Contents
--------
1. Definition and Architecture
    * Definition
    * Architecture
    
2. OpenStack Services Types and Brief Definition
    1. Keystone
    2. Glance    
    3. Placement
    4. Nova  
    5. Neutron
    
3. Request Flow for Launching an Instance in OpenStack

---

### 1. Definition and Architecture
* Definition
    The OpenStack Project is an open source cloud computing platform that supports all types of cloud environments.
* Architecture
    - Conceptual Architecture   
    
        The below diagram shows the relationships among the OpenStack services.
        ![Conceptual Architecture](/Conceptual_Architecture.png)
        
    - Provider Network Architecture
    
        Below is the service layout of provider networks.
        ![Provider Network Service Layout](/Provider_Network.png)
        
        There are two networking options; provider network and self-service network. Provider networks lack support for self-service (private) networks, layer-3 (routing) services, and advanced services such as LBaaS [^1] and FWaaS [^2]. For future developments, it is necessary to use provider networks. Further explanations are in ['Neutron'](#Neutron) under ['OpenStack Services Types and Brief Definition'](#2-OpenStack-Services-Types-and-Brief-Definition).

[//]: # (Successfuly uploaded image)

---

### 2. OpenStack Services Types and Brief Definition
There are various kinds of services in OpenStack. As a minimum, the following services are essential when you launch an OpenStack project.
* #### Keystone ####
    Keystone is an identity service in OpenStack. It manages authentication and authorization of services required in cloud needs. Each OpenStack service in the deployment needs a service entry with corresponding endpoints stored in the Identity Service. 
* #### Glance ####
    Glance is an image service that enables users to discover, register, and retrieve virtual machine images. It supports the storage of disk or server images on various repository types. The OpenStack image service includes glance-API and glance-registry. Glance-API accept image API calls for image discovery, retrieval, and storage. Glance-registry stores, processes, and retrieves metadata about size and types of images. The image metadata is in the database, in my case, MariaDB. Exposing glance-registry to users is unnecessary, for it is a private internal service.
* #### Placement ####
    The placement API service was introduced within the nova repository and extracted to the placement repository in the Stein release. It is used to track resource provider inventories and usages. Placement is required by some of the other OpenStack services, notably nova. Two processes, Nova-compute and Nova-scheduler, host most of Nova's interaction with Placement.
* #### Nova ####
    Openstack Compute is used to host and manage cloud computing systems. Nova consists of the following areas and their components.

    **Nova-API Service**
    : Accepts and responds to end user compute API calls. The service supports the OpenStack Compute API. It enforces some policies and initiates most orchestration activities, such as running an instance.
    
    **Nova-compute Service**
    : A worker daemon that creates and terminates virtual machine instances through hypervisor APIs.
    
    **Nova-scheduler Service**
    : Takes a virtual machine instance request from the queue and determines on which compute server host it runs.
    
    **Nova-conductor Module**
    : Mediates interactions between the nova-compute service and the database. It eliminates direct accesses to the cloud database made by the nova-compute service. 
    
    **Nova-novncproxy Daemon**
    : Provides a proxy for accessing running instances through a VNC connection. Supports browser-based novnc clients.
    
* #### Neutron ####
    Neutron is a networking service in OpenStack. It allows you to create and attach interface devices managed by other OpenStack services to networks. The neutron-server accepts and routes API requests to the appropriate OpenStack Networking plug-in for action. Plugging and unplugging ports, creating networks or subnets, and providing IP addresses are capable. To route information between the neutron-server and various agents, the messaging queue(RabbitMQ) is used. It also acts as a database to store networking state for particular plug-ins.
    
    Any given Networking set up has on or more external and internal networks. IP addresses are accessible by anyone who is physically on the external network. Internal networks connect directly to the VMs. For the outside networks to access VMs, and vice versa, routers between the networks are needed. Each router has a gateway that connects to an external network and one or more interfaces connected to internal networks. 
    
	Between two network options, I will configure with provider networks. Provider networks map to actual physical networks or VLANs and can only be set up by an admin.
    
    **ML2 plug-in**
    To set up a provider network, first, configure the Modular Layer 2 (ML2) plug-in. The ML2 plug-in uses the Linux bridge mechanism to build layer-2, bridging and switching, virtual networking infrastructure for instances. Beyond various type drivers, flat and VLAN are enable. Flat networks make every instance in the same network. For example, if the compute node and the network node is using 20.20.20.0/24, the virtual machine will also have the same network. ML2 plug-in also provides the mechanism driver. A mechanism driver makes the system able to connect two other compute nodes with different networks. Linux bridge mechanism is the mechanism driver used.
    After completing the setup of the plug-in, the configuration of the Linux bridge agent, DHCP agent, and metadata agent is necessary.
    **Neutron-Linuxbridge agent**
    An L2 agent makes and stabilizes the virtual infrastructure. There are OVS(Open vSwitch) and Linux-bridge as kinds of L2 agents. Between the two of them, the Linux-bridge agent is a virtual interface that connects various network interfaces. Libvirt interacts with the Linux-bridge agent. Libvirt is a virtualized library API, and the usage is when interaction with hypervisors, that support OpenStack, is needed. 
    **Neutron-DHCP agent**
    Neutron DHCP agent has a role that assigns IP addresses to the VMs located on the virtual network using dnsmasq.
    **Neutron-metadata Agent**
    The metadata agent provides IP address or instance information that is needed while booting VM instance.
    
    To verify the successful launch of the neutron agents, use the command below.
    ~~~
    [root@controller ~]# openstack network agent list
    ~~~
    If the networking service successfully installed, the output should indicate three agents on the controller node and one agent on each compute node.

[//]: # (When opening file in Github, change [^1] to <sup>1</sup>)

---

### 3. Request Flow for Launching an Instance in OpenStack

Below is the diagram that shows the request flow when launching an instance in OpenStack.
![Request Flow for Launching Instance](/Request_Flow_Diagram.PNG)

The diagram can be split into two big blocks; transformation of CLI request to running instances (Nova), network connections between compute nodes and instances (Neutron).

+ #### Transformation of CLI request to running instances ####
    Three nova packages on the controller side; nova-API, nova-conductor, nova-scheduler; are related to creating instances. Nova-compute on the compute node supports several hypervisors to deploy instances or VMs. 
    
    Nova-API's role in creating an instance is it launches a new situation. Nova-scheduler searches for the appropriate host to install the VM and nova-conductor connect between database and nova-compute. The below diagram shows the connection between each service.
    ![Transformation of CLI request to running instances](/Nova_Request_Flow.png)
    1. Client requests for authentication to Keystone / Keystone pass authentication token to Client
    2. Client converts new instance request to REST API request and sends it to nova-API
    3. Nova-API receives the request and sends the request to Keystone to validate auth-token / Keystone confirms the token and sends it back
    4. Nova-API interacts with the database ( MariaDB ) to create initial DB entry for a new instance
    5. Nova-API sends the rpc.call request by message queue ( RabbitMQ ) to nova-scheduler to get updated instance entry with host ID specified
    6. Nova-scheduler picks the request from the queue
    7. Nova-scheduler interacts with the database to find  an appropriate host
    8. Nova-scheduler sends the rpc.cast by the message queue to nova-compute for launching the instance on a suitable host
    9. Nova-compute picks the request from the queue and sends the rpc.call request to nova-conductor to fetch the instance information
    10. Nova-conductor picks the request from the queue
    11. Nova-conductor interacts with the database and returns the instance information
    12. Nova-conductor sends the rpc.cast by the message queue to nova-compute for returning the instance information
    13. Nova-compute picks the instance information from the queue

+ #### Network Connections between compute nodes and instances ####
    qwer
    ![Network Connections between Commpute Nodes and Instances](/Neutron_Request_Flow.PNG)
    1. Nova-compute passes auth-token to Neutron-server to allocate and configure the network for the instance
    2. Neutron-server sends auth-token to Keystone for validation / Keystone confirms the token and sends it back
    3. Neutron-server sends the rpc.call request by message queue to request an IP address and L2 configuration
    
	**The request of the IP address**
    
    4. Neutron-DHCP-Agent picks the request from the queue
    5. Neutron-DHCP-Agent interacts with dnsmasq to allocate the IP address
    6. Neutron-DHCP-Agent returns the IP address information
    7. Neutron-server reads the IP address from the message queue
    
	**The request of L2 configuration**
    
    8. Neutron-LinuxBridge-Agent picks the request from the queue
    9. Neutron-LinuxBridge-Agent interacts with libvirt to configure Linux bridge
    10. Neutron-LinuxBridge-Agent returns the Linux bridge configuration
    11. Neutron-server reads the configuration from the message queue
    12. Neutron-server saves instance network state in the database
    13. Neutron-server passes the network information to Nova-compute

[^1]: Load Balance as a Service
[^2]: Firewall as a Service
