OpenStack
=====
목차 
--------
1. 정의 및 구조 
    * 오픈스택의 정의 
    * 오픈스택의 구조 
2. 오픈스택 서비스 종류 및 정의 
    1. Keystone
    2. Glance    
    3. Placement
    4. Nova  
    5. Neutron
    6. Cinder
3. 오픈스택에 인스턴스 설치 과정
    1. CLI Request로 인스턴스가 설치되는 과정 
    2. 컴퓨트 노드와 인스턴스 사이의 네트워크 연결 
    3. 새로운 인스턴스와 기타 서비스들과의 연결 과정 

---

### 1. 정의 및 구조 
* 오픈스택의 정의 
    오픈스택이란 프로젝트는 모든 종류의 클라우드를 위한 오픈 소스 클라우드 컴퓨팅 플랫폼이다.
* 오픈스택의 구조 
    - 개념적 구조   
    
        아래 다이어그램은 오픈스택 서비스들 간의 관계를 보여준다.
        ![Conceptual Architecture](/Conceptual_Architecture.png)
        
    - Provider Network Architecture
    
        아래는 프로바이더 네트워크의 서비스 레이아웃을 보여주는 이미지이다.
        ![Provider Network Service Layout](/Provider_Network.png)

        오픈스택을 이용해 인스턴스를 설치하기 위해서는 최소한 두 개의 노드를 필요로 한다. 상단의 이미지에서 볼 수 있듯이, 컨트롤러 노드는 인증 서비스, 이미지 서비스, 컴퓨트에 대한 관리, 네트워크 관리, 네트워크 에이전트들, 대시보드 등을 구동한다.또한 데이터베이스, 메시지큐, NTP와 같이 구동의 지원을 해주는 서비스들도 컨트롤러 노드에 포함된다. 컴퓨트 노드는 인스턴스를 작동하는 하이퍼바이저를 포함하고 있다. 이 노드는 인스턴스들과 VM을 연결해주는 네트워크 서비스 에이전트들 역시 포함한다.
        
        네트워크 방식으로는 프로바이더 네트워크와 셀프 서비스 네트워크가 존재한다. 프로바이더 네트워크는 셀프서비스 네트워크보다 지원되는 서비스들이 적은데, 그 서비스들로는 layer-3 서비스, 혹은 LBaas<sup>1</sup>와 FWaaS<sup>2</sup>와 같은 고급 서비스들이 있다. 추푸 개발을 위해 프로바이더 네트워크를 사용하도록 할 것이다. 자세한 설명은 ['Neutron'](#Neutron)에서 찾을 수 있다. 
        
---

### 2. 오픈스택 서비스 종류 및 정의 

오픈스택에는 다양한 종류의 서비스들이 존재한다. 그 중 오픈스택 프로젝트를 생성하는 데 필수적으로 필요한 서비스들에 대해서만 설명하도록 하겠다.
* #### Keystone ####
    Keystone은 오픈스택의 인증 서비스이다. 이 서비스는 클라우드가 필요로 하는 서비스들에 대한 인증과 권한을 부여해주는 역할을 가지고 있다. 모든 오픈스택 서비스들은 Keystone을 거쳐야만 자원을 사용할 수 있다.
* #### Glance ####
    Glance는 사용자들이 VM의 이미지의 삭제ㆍ정보ㆍ수정 등 관리를 할 수 있도록 하는 서비스이다. 여기서 이미지란, 인스턴스에 필요한 운영체제가 설치된 이미지를 뜻한다. 이 서비스는 다양한 리포지토리의 서버 이미지 저장을 지원한다. Glance는 Glance-API와 Glance-registry로 구성되며, Glance-API는 이미지 삭제ㆍ정보ㆍ수정에 대한 API 요청을 수락하는 역할을 한다. Glance-registry는 크기 및 이미지 종류와 같은 메타데이터의 삭제ㆍ정보ㆍ저장을 맡고 있다. 이미지 메타데이터의 경우, 데이터베이스에 저장되어 있는데, 해당 프로젝트에서는 MariaDB를 사용한다. Glance-registry는 사용자에게 권한이 없는 서비스이다.
* #### Placement ####
    Placement 서비스는 초기에 Nova 내부에 존재하던 서비스이며, Stein 버전에서 별도의 서비스로 소개되었다. 이 서비스는 리소스 프로바이더에 대한 인벤토리와 사용정보를 추적하는 데 사용된다. Placement는 주로 다른 서비스들이 요구하는 데, 특히 Nova에서 필요로 하는 서비스이다. Nova-compute, Nova-scheduler과 같은 프로세스들이 대표적으로 Placement를 이용한다.
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

* #### Cinder ####
    Cinder은 오픈스택의 블록 스토리지 서비스이다. 블록 스토리지는 volume을 관리하는 인프라를 제공하고 Openstack 컴퓨팅과 상호작용하여 인스턴스의 volume을 생성한다. 이 서비스는 또한 볼륨 스냅 샷 및 볼륨 유형을 관리 할 수 있게 한다. Cinder 구성은 빈 로컬 블록 저장 장치가있는 하나의 스토리지 노드를 참조한다.

[//]: # (When opening file in Github, change [^1] to <sup>1</sup>)

---

### 3. 오픈스택에 인스턴스 설치 과정

아래는 오픈스택에 인스턴스를 설치하는 과정을 보여주는 다이어그램이다.
![Request Flow for Launching Instance](/Request_Flow_Diagram.PNG)

오픈스택에 인스턴스를 설치하는 과정은 크게 CLI Request로 인스턴스가 설치되는 과정 (Nova), 컴퓨트 노드와 인스턴스 사이의 네트워크 연결 (Neutron)으로 나눌 수 있다. 이 두 과정을 설명하기에 앞서, 메시지큐를 이용하여 두 가지 요청이 일어나는데, RPC.call과 RPC.cast라고 하는 것들이다. 간단히 설명하자면, RPC.call은 대답을 요구하고, RPC.cast는 대답을 요구하지 않는다. 아래는 예시이다.
> Nova-API는 nova-scheduler에게 인스턴스를 설치할 노드 정보를 받아오도록 RPC.call을 보낸다.

Nova-API는 nova-scheduler에게 RPC.call을 보냈기에, nova-scheduler은 인스턴스가 설치될 노드 정보를 반환하여 nova-API에게 전달할 것이다.

> Nova-scheduler은 nova-compute에게 인스턴스를 적절한 노드에 설치하도록 RPC.cast를 요청한다.

RPC.cast는 따로 응답을 요구하지 않으므로, 위의 요청을 하였을 때 nova-scheduler에게 별도의 정보가 오지 않고 인스턴스는 설치될 것이다.

+ #### CLI Request로 인스턴스가 설치되는 과정 ####
    컨트롤러 노드에서는 nova-API, nova-conductor, nova-scheduler이 새로운 인스턴스를 생성하는 데 연관이 있다.  컴퓨트 노드의 Nova-compute는 각종 하이퍼바이저를 지원한다. 
    Nova-API의 역할은 새로운 인스턴스를 설치하는 것이다. Nova-scheduler은 인스턴스를 설치할 적절한 호스트를 검색하는 것, nova-conductor의 역할은 데이터베이스와 nova-compute 사이에서 정보를 전달해주는 것이다. 아래 다이어그램은 각 서비스들의 연결 상태를 보여준다.
    ![Transformation of CLI request to running instances](/Nova_Request_Flow.png)
    1. Client는 Keystone에게 인증을 요청한다 / Keystone는 인증된 토큰을 Client에게 넘겨준다
    2. Client는 새로운 인스턴스 요청을 REST API 요청으로 전환해 Nova-API에게 전달한다
    3. Nova-API는 요청을 전달받은 후 Keystone에게 인증을 요청한다 / Keystone는 인증된 토큰을 Nova-API에게 넘겨준다
    4. Nova-API는 데이터베이스로 새로우 인스턴스에 대한 DB 정보를 생성한다
    5. Nova-API는 nova-scheduler에게 인스턴스를 설치할 노드 정보를 받아오도록 RPC.call을 보낸다
    6. Nova-scheduler는 메시지큐에서 요청을 받아온다
    7. Nova-scheduler는 데이터베이스에서 알맞은 호스트 정보를 검색한 후 반환한다
    8. Nova-scheduler은 nova-compute에게 인스턴스를 적절한 노드에 설치하도록 RPC.cast를 요청한다
    9. Nova-compute는 메시지큐에서 요청을 읽어들인 후 nova-conductor에게 인스턴스 정보를 요청하는 RPC.call을 보낸다
    10. Nova-conductor는 메시지큐에서 요청을 읽어들인다
    11. Nova-conductor는 데이터베이스에서 인스턴스 정보를 가져와 반환한다
    12. Nova-conductor는 메시지큐를 통해 nova-compute로 인스턴스 정보에 대한 RPC.cast를 요청한다
    13. Nova-compute는 메시지큐에서 요청을 읽어들인다

+ #### 컴퓨트 노드와 인스턴스 사이의 네트워크 연결 ####
    Neutron은 오픈스택의 네트워크 서비스이다.
    Neutron-DHCP-Agent과 Neutron-Linuxbridge-Agent는 새로운 인스턴스를 설치하는 데 필요한 주요 인자들이다.  Neutron-DHCP-Agent는 dnsmasq에 연결해 VM에 IP 주소를 할당해주며, Neutron-Linuxbridge-Agent는 libvirt와 연결한다. Libvirt는 오픈스택을 지원하는 하이퍼바이저들과 상호작용하는 가상화 라이브러리 API이다. 
    ![Network Connections between Commpute Nodes and Instances](/Neutron_Request_Flow.PNG)
    1. Nova-compute는 인스턴스의 네트워크를 할당 및 구성해주기 위해 Neutron-server에게 auth-token을 넘겨준다
    2. Neutron-server는 인증을 위해 auth-token을 Keystone에게 보낸다 / Keystone은 해당 토큰을 인증해주고 Neutron-server로 반환한다
    3. Neutron-server은 메시지큐에게 IP 주소와 L2 구성을 요청하는 RPC.call을 보낸다
    
	**IP 주소 요청**
    
    4. Neutron-DHCP-Agent는 메시지큐에서 요청을 가져온다
    5. Neutron-DHCP-Agent는 dnsmasq와 연결하여 IP주소를 할당한다
    6. Neutron-DHCP-Agent는 IP 주소 정보를 반환한다
    7. Neutron-server는 메시지큐를 통해 정보를 읽어들인다
    
	**L2 구성 요청**
    
    8. Neutron-Linuxbridge-Agent는 메시지큐에서 요청을 가져온다
    9. Neutron-Linuxbridge-Agent는 libvirt와 연결하여 Linux bridge를 구성한다
    10. Neutron-Linuxbridge-Agent는 Linux bridge configuration를 반환한다
    11. Neutron-server는 메시지큐로부터 정보를 읽어들인다
    12. Neutron-server는 인스턴스 네트워크 상태를 데이터베이스에 저장한다
    13. Neutron-server는 네트워크 정보를 Nova-compute에 넘겨준다
     
+ #### 새로운 인스턴스와 기타 서비스들과의 연결 과정 ####
    **Glance**
    1. Nova-compute는 Glance로부터 이미지 URI를 가져오도록 glance-API에게 요청한다
    2. Glance-API는 keystone을 통해 auth-token 인증을 받는다 
    3. Glance-API는 Nova-compute에게 image-URI를 보내준다

    **Cinder**
    1. Nova-compute는 Cinder에게 volume 정보를 요청한다
    2. Cinder-API는 keystone을 통해 auth-token 인증을 받는다
    3. Cinder-API는 Nova-compute에게 volume 정보를 보내준다
    
---

<sup>1</sup> Load Balance as a Service
<p></p>
<sup>2</sup> Firewall as a Service
