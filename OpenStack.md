---
marp: true
theme: e_default
paginate: true
_paginate: false
---

# OpenStack

---

# Contents 

#### OpenStack Trend & Structure
#### OpenStack Feature
#### Request Flow when Launching an Instance
#### OpenStack Demo

---

# OpenStack Trend & Structure

---

### OpenStack Trend & Structure

![OpenStack Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Openstack_Structure.png)

[//]: # ( Horizon - Web Frontend : 대시보드 )
[//]: # ( EC2API - 오픈스택의 Amazon EC2API 서비스에 대한 호환성 계층 )
[//]: # ( o Magnum - Container 관리 서비스 ) 
[//]: # ( o Trove - 데이터베이스 관리 서비스 )
[//]: # ( Sahara - Hadoop과 같은 빅 데이터 어플리케이션을 쉽게 제공할 수 있게 도와주는 서비스 )
[//]: # ( Murano - 어플리케이션 카탈로그 서비스 )
[//]: # ( Freezer - 복원 및 백업 서비스 )
[//]: # ( Solum - redhat의 OpenShift와 같은 역할 : 컨테이너 기반 소프트웨어의 관리를 위한 레드햇의 소프트웨어 제품)
[//]: # ( Masakari - 실패한 인스턴스의 자동 복구로 인스턴스 고 가용성 서비스)
[//]: # ( o Heat - 오케스트레이션 서비스 : 오케스트레이션 - 자원 관리, 배치, 정렬을 자동화하는 것 )
[//]: # ( Mistral - 워크플로우를 관리하는 서비스)
[//]: # ( Aodh - Telemetry Alarming 서비스 : 수집된 미터 또는 이벤트 데이터가 정의된 규칙을 위반하는 경우 알림을 트리거 )
[//]: # ( Senlin - 오픈스택 클라우드를 위한 클러스터링 서비스 )
[//]: # ( Zaqar - 메시징 서비스 )
[//]: # ( Blazar - 오픈스택의 자원 예약 서비스 : 특정 자원을 특정 시간동안 사용자에게 할당해주는 서비스 )
[//]: # ( o Zun - 컨테이너 서비스 : 서버나 클러스터 관리를 하지 않고 컨테이너 시작, 구동할 수 있게 해줌 )
[//]: # ( o Qinling - Function as a Service )
[//]: # ( Octavia - Load Balancing : Load Balancing - 하나의 인터넷 서비스가 발생하는 트래픽이 많을 때 여러 서버가 분산처리해서 해결하는 것 )
[//]: # ( o Designate - DNS 서비스 : 도메인 및 레코드를 관리 / 다중 사용자 지원 등의 서비스 제공 )
[//]: # ( Tacker - NFV 서비스 : Network Functions Virtualization - 네트워크 기능을 추상화하여 표준화된 컴퓨팅 노드에서 실행되는 소프트웨어를 통해 네트워크 기능을 설치, 제어 및 조작하도록 지원 )
[//]: # ( o Ironic - 베어메탈 서비스 : 베어메탈 서비스 - 별도의 소프트웨어를 탑재하지 않은 클라우드 서비스 )
[//]: # ( Cyborg - 처리 능력을 가속화시키기 위한 하드웨어 사용을 가능하게 하는 서비스 )
[//]: # ( Manila - 파일 공유 서비스 : VM들 간의 파일 공유 )
[//]: # ( Barbican - 키 관리, 보안을 저장하고 관리하려고 설계된 서비스 )
[//]: # ( o Searchlight - 검색 기능 )
[//]: # ( Karbor - 데이터 보호 및 복원 기능 )
[//]: # ( Kuryr - 쿠버네티스 컨테이너 오케스트레이션과 연동할 수 있도록 하는 서비스 )
[//]: # ( Ceilometer - 클라우드에서 배포된 자원의 사용량과 성능을 측정해 사용자가 자원 상태를 모니터링할 수 있는 기능을 제공 )
[//]: # ( Monasca - 클라우드 서비스 장애나 성능을 모니터링하기 위한 서비스 )
[//]: # ( Watcher - multi-tenant 오픈스택 기반의 클라우드를 위한 유연하고 확장 가능한 리소스 optimization 서비스를 제공 )
[//]: # ( Congress - 클라우드를 위한 공개 정책 프레임워크 : admin은 정책을 정의하거나 모니터링이 가능 )
[//]: # ( CloudKitty - 오픈스택의 Rating-as-a-Service : 수치 확인을 할 수 있는 서비스 )
[//]: # ( Tricircle - Neutron의 네트워킹 자동화를 제공하는 서비스)
---

### OpenStack Trend & Structure

[//]: # (Console -> management console)
[//]: # (CLI->AWS CLI)
[//]: # (AWS와 openstack의 가장 큰 차이점 : network 쪽 서비스 X - Kuryr&Tacker이 AWS에는 없음)
[//]: # (Cloud Watch 등 AWS 서비스들 검색)

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/0.png)

---

### OpenStack Trend & Structure

[//]: # ( OpenStack CLI -> AWS ClI)

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/01.png)

---

### OpenStack Trend & Structure

[//]: # ( Horizon -> Management Console )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/02.png)

---

### OpenStack Trend & Structure

[//]: # ( Magnum -> ECS )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/03.png)

---

### OpenStack Trend & Structure

[//]: # ( Trove -> RDS )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/04.png)

---

### OpenStack Trend & Structure

[//]: # ( Sahara -> EMR )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/05.png)

---

### OpenStack Trend & Structure

[//]: # ( Heat -> Cloud Formation )
[//]: # ( Mistral -> SWF )
[//]: # ( Zaqar -> SQS )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/06.png)

---

### OpenStack Trend & Structure

[//]: # ( Nova -> EC2 )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/07.png)

---

### OpenStack Trend & Structure

[//]: # ( Zun -> Fargate )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/08.png)

---

### OpenStack Trend & Structure

[//]: # ( Qinling -> Lambda )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/09.png)

---

### OpenStack Trend & Structure

[//]: # ( Neutron -> Networking )
[//]: # ( AWS에는 Container 서비스 / NFV 서비스가 별도로 존재하지 않음 -> 네트워크 부분에서 OpenStack의 활용도가 더 높음 )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/10.png)

---

### OpenStack Trend & Structure

[//]: # ( Octavia -> ELB )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/11.png)

---

### OpenStack Trend & Structure

[//]: # (Designate -> Route 53)

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/12.png)

---

### OpenStack Trend & Structure

[//]: # ( Swift -> S3 )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/13.png)

---

### OpenStack Trend & Structure

[//]: # ( Cinder -> EBS )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/14.png)

---

### OpenStack Trend & Structure

[//]: # ( Manila -> EFS )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/15.png)

---

### OpenStack Trend & Structure

[//]: # ( Keystone -> IAM )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/16.png)

---

### OpenStack Trend & Structure

[//]: # ( Glance -> Amazon Machine Images )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/17.png)

---

### OpenStack Trend & Structure

[//]: # ( Barbican -> KMS )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/18.png)

---

### OpenStack Trend & Structure

[//]: # ( Searchlight -> Elasticsearch )

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/19.png)

---

### OpenStack Trend & Structure

[//]: # ( Ceilometer -> Cloudwatch )
[//]: # ( CloudKitty -> AWS Usage and Billing Report)

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/20.png)

---

[//]: # (실제 network상 구조)
[//]: # (node내 사용되는 feature들 연결해서 강조하여 보여주기)

### OpenStack Project Architecture

![width:1000px](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_Full_Diagram.png)

---

# OpenStack Features

---

![width:500 bg right:55%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/PN_Keystone.png)

# Keystone

[//]: # ( 네트워크 구성은 두 가지 : 프로바이더, 셀프 서비스가 존재 -> 그 중 프로바이더 네트워크로 구축할 것 )
[//]: # ( 프로바이더 네트워크일 때 컨트롤러 노드 / 컴퓨트 노드 내 포함된 서비스들 제시 )
[//]: # ( 컨트롤러 노드 : 네트워크 관리, 컴퓨트에 대한 관리, 인증 / 이미지 서비스 등 각종 서비스와 메시지큐나 DB와 같은 지원을 해주는 서비스들 포함 )
[//]: # ( 컴퓨트 노드 : 인스턴스를 실행시키는 하이퍼바이저, Linuxbridge Agent로 인스턴스와 노드를 연결 )
[//]: # ( 노드 내 서비스들을 순서대로 소개 )

---

![width:500 bg right:46%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Keystone_Auth.png)

## Keystone

- **오픈스택의 인증 서비스**
    클라우드가 필요로 하는 서비스들에 
    대한 인증과 권한을 부여해주는 역할

---

![width:500 bg right:46%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Nova_Endpoint_Structure.png)

## Keystone

[//]: # ( ***하위 설명 / 그림 속 노드들은 Keystone의 구성요소*** )
[//]: # ( Tenant : 어떤 자원이나 어플리케이션에 대한 권리를 가진 보안 그룹 )
[//]: # ( User : 사용자 계정 정보 / Role : 사용자 권한 )
[//]: # ( Token : 사용자가 오픈스택 서비스가 제공하는 자원에 접근할 때 신분을 증명하기 위해 사용하는 데이터 )
[//]: # ( User은 Role을 가지며, Token을 발행받기 위해서는 Tenant와 User 정보가 필요함 )
[//]: # ( Endpoint : 사용자가 서비스를 이용하기 위해 연결 정보를 제공하는 접근 가능한 네트워크 주소 )

- **오픈스택의 인증 서비스**
    클라우드가 필요로 하는 서비스들에 
    대한 인증과 권한을 부여해주는 역할

---

![width:500 bg right:55%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/PN_Glance.png)

# Glance

---

![width:500 bg right:46%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Glance_Structure.png)

## Glance

[//]: # ( Glance-API, Glance-Registry, Database로 구성 )
[//]: # ( Glance-API : 이미지를 등록, 삭제 등 관리 )
[//]: # ( 이미지의 등록 : Glance-Registry를 통해 Database에 등록 )
[//]: # ( 이미지의 사용 : Glance-API에서 Database로 직접 사용 요청 )

- **오픈스택의 이미지 관리 서비스**
    사용자들이 VM 이미지의 삭제, 수정, 조회 등 관리를 할 수 있도록 하는 
    서비스
---

![width:500 bg right:55%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/PN_Nova.png)

# Nova / Placement

---

![width:500 bg right:45%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Nova_Structure.png)

[//]: # ( Nova-API : 사용자의 컴퓨팅 API 호출을 수락하고 응답 )
[//]: # ( Nova-Scheduler : 인스턴스를 어느 컴퓨트 노드에 설치할지 결정하는 서비스 )
[//]: # ( Nova-Conductor : Nova-compute와 Database 간의 상호작용 )
[//]: # ( Nova-Compute : 가상 머신 인스턴스를 작성하고 종료하는 서비스 )
[//]: # ( Nova-novncproxy : VNC 연결을 통해 실행 중인 인스턴스에 엑세스하기 위한 프록시를 제공 )

## Nova

- **오픈스택의 컴퓨팅 서비스**
    클라우드 컴퓨팅 시스템을 호스팅하고 관리

## Placement

- 리소스 프로바이더에 대한 인벤토리와 사용 정보를 추적하는 데 사용

---

![width:500 bg right:48%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/PN_Neutron.png)

# Neutron

---

![width:500 bg right:48%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/PN_Neutron.png)

## Neutron

[//]: # ( 프로바이더 네트워크, 셀프 서비스 네트워크 둘 중 프로바이더 네트워크를 구축할 것 )

[//]: # ( ML2 Plug-in : ML2 플러그인은 인스턴스를 위한 Layer-2; Bridging & Switching; 가상 네트워크 인프라를 구축 )
[//]: # (               Type drivers 중 flat와 VLAN을 사용 -> flat : 모든 인스턴스를 같은 네트워크 상에 있도록 하는 것 )
[//]: # (               메커니즘 드라이버 제공 -> 메커니즘 드라이버 : 각각 다른 네트워크를 사용하는 컴퓨트 노드들의 연결이 가능하도록 함 )

[//]: # ( Linuxbridge Agent : L2 에이전트의 종류 중 하나 -> L2 에이전트 - 가상 인프라를 생성 및 안정화하는 역할 // Linuxbridge와 Open vSwitch // )
[//]: # (                     Linuxbridge는 다양한 네트워크 인터페이스를 연결해주는 가상의 인터페이스 )
[//]: # (                     Libvirt와 상호작용 -> Libvirt : 오픈스택을 지원하는 하이퍼바이저와의 소통이 필요할 때 이용 )

[//]: # ( DHCP Agent : dnsmasq를 이용해 가상 네트워크에 위치한 인스턴스들에게 IP 주소를 할당해주는 역할 )

[//]: # ( Metadata Agent : 인스턴스가 부팅되는 데 필요한 IP 주소와 인스턴스 정보를 제공 )

- **오픈스택의 네트워킹 서비스**
    다른 오픈스택 서비스로 관리되는 인터페이스 장치를 생성하여
    네트워크에 연결할 수 있도록 하는 서비스

---

![width:500 bg right:50%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/PN_Cinder.png)

# Cinder

---

![width:500 bg right:47%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Cinder_Structure.png)

## Cinder

- **오픈스택의 블록 스토리지 서비스**
    볼륨을 관리하는 인프라를 제공하고 인스턴스의 볼륨을 생성

    [//]: # ( 볼륨을 관리하는 인프라를 제공, 오픈스택 컴퓨팅과 상호작용하여 인스턴스의 볼륨을 생성 -> 볼륨을 관리하는 것 또한 Cinder의 역할 )

---

# Request Flow when Launching an Instance

---

### Request Flow when Launching an Instance

[//]: # ( Request Flow는 크게 두 가지 과정으로 나눔 -> Nova : CLI 요청을 받았을 때 인스턴스 설치 )
[//]: # (                                            Neutron : 설치된 인스턴스의 네트워크 연결 )

![width:8540px](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Request_Flow_Diagram.png)

---

### Transformation of CLI Request to Running Instances

[//]: # ( CLI의 Keystone 인증 요청 / 인증된 token 반환 )
[//]: # ( CLI가 Nova-API에게 새로운 인스턴스 설치 요청 )
[//]: # ( Nova-API의 Keystone 인증 요청 / 인증된 token 반환 )
[//]: # ( Nova-API가 Database에 새로운 인스턴스에 대한 DB 정보를 생성 )
[//]: # ( Nova-API가 Nova-Scheduler에게 인스턴스를 설치할 노드 정보를 받아오도록 RPC.Call을 message queue로 전송 )
[//]: # ( Nova-Scheduler이 요청을 message queue에서 받아 옴 )
[//]: # ( Nova-Scheduler이 Database에서 알맞는 호스트 정보를 검색 후 반환 )
[//]: # ( Nova-Schduler에서 Nova-Compute로 인스턴스를 검색한 노드에 설치하도록 message queue를 통해 RPC.Cast를 전송 )
[//]: # ( Nova-Compute는 요청을 message queue에서 받아 옴 )
[//]: # ( Nova-Compute는 Nova-Conductor에게 인스턴스 정보를 요청하는 RPC.Call을 message queue로 전송 )
[//]: # ( Nova-Conductor이 요청을 message queue에서 받아 옴 )
[//]: # ( Nova-Conductor은 Database에서 인스턴스 정보를 받아와 Nova-Compute로 반환 )

![bg right width:600px](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Nova_Request_Flow.png)

---

### Network Connections between Compute Nodes and Instances

[//]: # ( Neutron : Linuxbridge Agent - libvirt와 연결해 L2 ;Linuxbridge; 구성 )
[//]: # (           DHCP Agent - dnsmasq와 연결해 인스턴스에 IP 주소를 할당 )
[//]: # ( Nova-Compute는 Neutron-Server에게 인스턴스의 네트워크 할당 및 구성을 위한 요청 )
[//]: # ( Neutron-Server의 Keystone 인증 요청 / 인증된 token 반환 )
[//]: # ( Neutron-Server이 IP 주소의 할당과 L2 구성을 요청하는 RPC.Call을 message queue로 전송 )
[//]: # ( DHCP Agent이 요청을 message queue에서 받아 옴 )
[//]: # ( DHCP Agent와 dnsmasq의 연결로 IP 주소를 할당 후 반환 )
[//]: # ( Linuxbridge Agent이 요청을 message queue에서 받아 옴 )
[//]: # ( Linuxbridge Agent와 libvirt의 연결로 Linuxbridge를 구성 후 configuration을 반환)
[//]: # ( Neutron-Server은 정보들을 message queue로부터 받아 옴 )
[//]: # ( Neutron-Server은 인스턴스 네트워크 상태를 Database에 저장 )
[//]: # ( Neutron-Server은 네트워크 정보를 Nova-Compute에게 전달 )

![bg right width:600px](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Neutron_Request_Flow.png)

---

### Other Interactions between the New Instance and Components in OpenStack

[//]: # ( Nova-Compute는 Glance에게서 이미지 URI 요청 )
[//]: # ( Glance-API의 Keystone 인정 요청 / 인증된 token 반환 )
[//]: # ( Nova-Compute에게 이미지 URI 반환 )
[//]: # ( ------------------------------------------------- )
[//]: # ( Nova-Compute는 Cinder에게서 Volume 정보 요청 )
[//]: # ( Cinder-API의 Keystone 인증 요청 / 인증된 token 반환 )
[//]: # ( Nova-Compute에게 Volume 정보 반환 )

---

![bg right:59% width:500](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Demo_Network_Architecture.png)

# OpenStack Demo

[//]: # ( ***** Instance Actions ***** )
[//]: # ( Instance pause : 메모리에 VM의 상태를 저장 )
[//]: # ( Instance suspend : 디스크에 VM의 상태를 저장 )
[//]: # ( pause는 인스턴스의 백업을 필요로 할 때 / suspend는 인스턴스가 자주 사용되지 않을 때 사용 )
[//]: # ( Instance shelve : 인스턴스를 멈추고 스냅샷을 찍음 )
[//]: # ( -> 0 : 후에 하이퍼바이저에서 스냅샷이 삭제됨 )
[//]: # ( -> -1 : 스냅샷이 절대 삭제되지 않음 )
[//]: # ( -> >0 : 일정 시간 후 스냅샷 삭제 )
 