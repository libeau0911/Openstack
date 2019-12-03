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
    
    오픈스택은 가상 리소스를 사용하여 모든 종류의 클라우드를 구축하고 관리하는 오픈소스 클라우드 컴퓨팅 플랫폼이다. 오픈스택 플랫폼을 포함하는 툴, 일명 프로젝트는 컴퓨팅, 네트워킹, 스토리지, Identity 및 이미지 서비스의 핵심 클라우드 컴퓨팅 서비스를 처리한다. 오픈스택의 활용방안으로는 프라이빗 클라우드, 퍼블릭 클라우드의 효율적인 구축, 네트워크 기능의 가상화 등이 있다. 
    
* 오픈스택의 구조 
    - 개념적 구조   
    
        오픈스택은 컴퓨팅, 네트워킹, 스토리지 등을 처리하는 핵심 서비스들을 중심으로, 대시보드, 오케스트레이션 등 부가적인 서비스들을 처리할 수 있도록 하는 인프라를 생성할 수 있다. 아래 다이어그램은 오픈스택 서비스들 간의 관계를 보여준다.
        ![Conceptual Architecture](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Conceptual_Architecture.png)
    
    - Provider Network Architecture
    
        아래는 프로바이더 네트워크의 서비스 레이아웃을 보여주는 이미지이다.
        ![Provider Network Service Layout](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Provider_Network.png)
        
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
    오픈스택 컴퓨트는 클라우드 컴퓨팅 시스템을 호스팅하고 관리하는 데 사용된다. Nova는 다음 영역과 해당 구성 요소로 구성된다.

    **Nova-API 서비스**
    
    해당 서비스는 사용자의 컴퓨팅 API 호출을 수락하고 응답한다. 이 서비스는 오픈스택 컴퓨트 API를 지원한다. 일부 정책을 시행하고 인스턴스 실행과 같은 대부분의 오케스트레이션 활동을 시행한다.
    
    **Nova-compute 서비스**
    
    하이퍼 바이저 API를 통해 가상 머신 인스턴스를 작성하고 종료하는 작업자 데몬이다.
    
    **Nova-scheduler 서비스**
    
    VM 인스턴스 요청을 메시지큐에서 가져와 어떤 컴퓨트 서버에서 실행할지 결정하는 서비스이다.
    
    **Nova-conductor 모듈**
    
    nova-compute 서비스와 데이터베이스 간의 상호 작용을 중재한다. 클라우드 데이터베이스에 대한 nova-compute의 직접적인 접근이 일어나지 않도록 한다.
    
    **Nova-novncproxy 데몬**
    
    VNC 연결을 통해 실행중인 인스턴스에 액세스하기 위한 프록시를 제공하며, 브라우저 기반 novnc 클라이언트를 지원한다.
    
* #### Neutron ####
    Neutron은 오픈스택의 네트워킹 서비스이다. 이 서비스는 다른 OpenStack 서비스로 관리되는 인터페이스 장치를 생성하여 네트워크에 연결할 수 있도록 한다. Neutron 서버는  API 요청을 승인하여 적절한 OpenStack Networking 플러그인으로 라우팅하여 조치를 취합니다. 이 서비스로 포트를 연결 및 분리, 네트워크 또는 서브넷을 생성, IP 주소를 제공하는 것이 가능하다. 또한 특정 플러그인의 네트워킹 상태를 저장하는 데이터베이스의 역할을 한다. Neutron server와 다양한 에이전트 간에 정보를 라우팅하기 위해서 메시지큐가 사용된다. 
    어떠한 네트워크 설정에는 하나 이상의 외부 및 내부 네트워크가 존재한다. IP 주소는 외부 네트워크에있는 모든 사람이 액세스 할 수 있는 반면, 내부 네트워크는 VM에 직접 연결이 된다. 외부 네트워크가 VM에 접근하거나 그 반대의 경우 네트워크 간의 라우터가 필요하다. 각 라우터에는 외부 네트워크에 연결되는 게이트웨이와 내부 네트워크에 연결된 하나 이상의 인터페이스가 있다.
    
    두 가지 네트워크 방식 중, 해당 프로젝트에서는 프로바이더 네트워크를 구성할 것이다. 프로바이더 네트워크는 실제 물리적인 네트워크 및 VLAN에 연결되며 admin에 의해서만 설정이 가능하다.
    
    **ML2 plug-in**
    
    프로바이더 네트워크를 설정하기 위해서는 먼저 Modular Layer 2 (ML2) 플러그인을 구성해야한다. ML2 플러그인은 Linux-bridge 메커니즘을 이용해 인스턴스를 위한 layer-2(브리징과 스위칭) 가상 네트워킹 인프라를 구축한다. 다양한 type drivers 중, flat와 VLAN이 사용가능하도록 설정한다. 플랫 네트워크는 모든 인스턴스를 같은 네트워크 상에 있도록 한다. 예를 들어, 컴퓨트 노드와 네트워크 노드가 20.20.20.0/24를 사용한다고 하였을 때, VM 역시 같은 네트워크 상에 존재하게 된다. ML2 플로그인은 메커니즘 드라이버도 제공한다. 메커니즘 드라이버는 각각 다른 네트워크를 사용하는 컴퓨트 노드들의 연결이 가능하도록 한다. 해당 프로젝트에서는 Linux-bridge 메커니즘을 사용하였다.
    플러그인 설정을 완료한 후에는 Linux-bridge 에이전트, DHCP 에이전트 및 메타데이터 에이전트를 구성해야한다.

    **Neutron-Linuxbridge agent**
    
    L2 에이전트는 가상 인프라를 생성 및 안정화하는 역할을 가지고 있다. L2 에이전트에는 OVS(Open vSwitch)와 Linux-bridge가 있는데, 둘 중 Linux-bridge는 다양한 네트워크 인터페이스를 연결하는 가상의 인터페이스다. Libvirt는 Linux-bridge와 상호작용하는 가상화 라이브러리 API이다. Libvirt은 오픈스택을 지원하는 하이퍼바이저와의 소통이 필요할 때 이용된다.
    
    **Neutron-DHCP agent**
    
    Neutron DHCP agent는 dnsmasq를 이용하여 가상 네트워크에 위치한 VM들에게 IP주소를 할당해주는 역할을 가지고 있다.
    
    **Neutron-metadata agent**
    
    메타데이터 에이전트는 VM 인스턴스를 부팅하는 데 필요한 IP 주소 및 인스턴스 정보를 제공해준다.
    
    Nuetron 에이전트들의 설치가 제대로 되었다는 것을 확인하고자 할 때, 아래의 명령어를 사용하면 된다.
    ~~~
    [root@controller ~]# openstack network agent list
    ~~~
    네트워킹 서비스가 성공적으로 설치되었으면, 결과화면으로 컨트롤러 노드에 세 에이전트, 컴퓨트 노드마다 하나의 에이전트가 표기되어야한다.

* #### Cinder ####
    Cinder은 오픈스택의 블록 스토리지 서비스이다. 블록 스토리지는 volume을 관리하는 인프라를 제공하고 Openstack 컴퓨팅과 상호작용하여 인스턴스의 volume을 생성한다. 이 서비스는 또한 볼륨 스냅 샷 및 볼륨 유형을 관리 할 수 있게 한다. Cinder 구성은 빈 로컬 블록 저장 장치가 있는 하나의 스토리지 노드를 참조한다.

[//]: # (When opening file in Github, change [^1] to <sup>1</sup>)

---

### 3. 오픈스택에 인스턴스 설치 과정

아래는 오픈스택에 인스턴스를 설치하는 과정을 보여주는 다이어그램이다.
![Request Flow for Launching Instance](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Request_Flow_Diagram.png)

오픈스택에 인스턴스를 설치하는 과정은 크게 CLI Request로 인스턴스가 설치되는 과정 (Nova), 컴퓨트 노드와 인스턴스 사이의 네트워크 연결 (Neutron)으로 나눌 수 있다. 이 두 과정을 설명하기에 앞서, 메시지큐를 이용하여 두 가지 요청이 일어나는데, RPC.call과 RPC.cast라고 하는 것들이다. 간단히 설명하자면, RPC.call은 대답을 요구하고, RPC.cast는 대답을 요구하지 않는다. 아래는 예시이다.
> Nova-API는 nova-scheduler에게 인스턴스를 설치할 노드 정보를 받아오도록 RPC.call을 보낸다.

Nova-API는 nova-scheduler에게 RPC.call을 보냈기에, nova-scheduler은 인스턴스가 설치될 노드 정보를 반환하여 nova-API에게 전달할 것이다.

> Nova-scheduler은 nova-compute에게 인스턴스를 적절한 노드에 설치하도록 RPC.cast를 요청한다.

RPC.cast는 따로 응답을 요구하지 않으므로, 위의 요청을 하였을 때 nova-scheduler에게 별도의 정보가 오지 않고 인스턴스는 설치될 것이다.

+ #### CLI Request로 인스턴스가 설치되는 과정 ####
    컨트롤러 노드에서는 nova-API, nova-conductor, nova-scheduler이 새로운 인스턴스를 생성하는 데 연관이 있다.  컴퓨트 노드의 Nova-compute는 각종 하이퍼바이저를 지원한다. 
    Nova-API의 역할은 새로운 인스턴스를 설치하는 것이다. Nova-scheduler은 인스턴스를 설치할 적절한 호스트를 검색하는 것, nova-conductor의 역할은 데이터베이스와 nova-compute 사이에서 정보를 전달해주는 것이다. 아래 다이어그램은 각 서비스들의 연결 상태를 보여준다.
    ![Transformation of CLI request to running instances](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Nova_Request_Flow.png)
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
    ![Network Connections between Commpute Nodes and Instances](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Neutron_Request_Flow.png)
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
