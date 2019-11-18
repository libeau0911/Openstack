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
    6. Cinder
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
* #### Keystone
    Keystone is an identity service in OpenStack. It manages authentication and authorization of services required in cloud needs. Each OpenStack service in the deployment needs a service entry with corresponding endpoints stored in the Identity Service. 
* #### Glance
    Glance is an image service that enables users to discover, register, and retrieve virtual machine images. It supports the storage of disk or server images on various repository types. The OpenStack image service includes glance-API and glance-registry. Glance-API accept image API calls for image discovery, retrieval, and storage. Glance-registry stores, processes, and retrieves metadata about size and types of images. The image metadata is in the database, in my case, MariaDB. Exposing glance-registry to users is unnecessary, for it is a private internal service.
* #### Placement
    The placement API service was introduced within the nova repository and extracted to the placement repository in the Stein release. It is used to track resource provider inventories and usages. Placement is required by some of the other OpenStack services, notably nova. Two processes, Nova-compute and Nova-scheduler, host most of Nova's interaction with Placement.
* #### Nova
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
    
* #### Neutron

[//]: # (Neutron is a networking service.)
* #### Cinder[^3]

[//]: # (Cinder is a block storage service.)
[//]: # (When opening file in Github, change [^1] to <sup>1</sup>)

---

### 3. Request Flow for Launching an Instance in OpenStack

Below is the diagram that shows the request flow when launching an instance in OpenStack.
![Request Flow for Launching Instance](/Request_Flow_Diagram.PNG)

The diagram can be split into two big blocks; transformation of CLI request to running instances (Nova), network connections between compute nodes and instances (Neutron).





[^1]: Load Balance as a Service
[^2]: Firewall as a Service
[^3]: Cinder is not essential when launching an instance, but this service is explained for it will be used in future developments. 

