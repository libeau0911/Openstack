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

[//]: # ( o Magnum - Container 관리 서비스 ) 
[//]: # ( o Trove - 데이터베이스 관리 서비스 )
[//]: # ( Sahara - Hadoop과 같은 빅 데이터 어플리케이션을 쉽게 제공할 수 있게 도와주는 서비스 )
[//]: # ( Murano - 어플리케이션 카탈로그 서비스 )
[//]: # ( Solum - redhat의 OpenShift와 같은 역할 : 컨테이너 기반 소프트웨어의 관리를 위한 레드햇의 소프트웨어 제품)
[//]: # ( o Heat - 오케스트레이션 서비스 : 오케스트레이션 - 자원 관리, 배치, 정렬을 자동화하는 것 )
[//]: # ( Senlin - 오픈스택 클라우드를 위한 클러스터링 서비스 )
[//]: # ( Zaqar - 메시징 서비스 )
[//]: # ( o Zun - 컨테이너 서비스 : 서버나 클러스터 관리를 하지 않고 컨테이너 시작, 구동할 수 있게 해줌)
[//]: # ( o Qinling - Function as a Service )
[//]: # ( Octavia - Load Balancing : Load Balancing - 하나의 인터넷 서비스가 발생하는 트래픽이 많을 때 여러 서버가 분산처리해서 해결하는 것 )
[//]: # ( o Designate - Domain Name Service )
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
[//]: # ( CloudKitty - 오픈스택의 Rating-as-a-Service : 수치 확인을 할 수 있는 서비스)

---

### OpenStack Trend & Structure

[//]: # (Console -> management console)
[//]: # (CLI->AWS CLI)
[//]: # (AWS와 openstack의 가장 큰 차이점 : network 쪽 서비스 X - Kuryr&Tacker이 AWS에는 없음)
[//]: # (Cloud Watch 등 AWS 서비스들 검색)

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/0.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/01.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/02.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/03.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/04.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/05.png)

---

### OpenStack Trend & Structure

[//]: # (Mistral -> SWF)
[//]: # (Zaqar -> SQS)

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/06.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/07.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/08.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/09.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/10.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/11.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/12.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/13.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/14.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/15.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/16.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/17.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/18.png)

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/OpenStack_to_AWS/19.png)

---

### OpenStack Trend & Structure

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

---

![width:500 bg right:46%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Keystone_Auth.png)

## Keystone

- **오픈스택의 인증 서비스**
    클라우드가 필요로 하는 서비스들에 
    대한 인증과 권한을 부여해주는 역할

---

![width:500 bg right:46%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Nova_Endpoint_Structure.png)

## Keystone

- **오픈스택의 인증 서비스**
    클라우드가 필요로 하는 서비스들에 
    대한 인증과 권한을 부여해주는 역할

---

![width:500 bg right:55%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/PN_Glance.png)

# Glance

---

![width:500 bg right:46%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Glance_Structure.png)

## Glance

- **오픈스택의 이미지 관리 서비스**
    사용자들이 VM 이미지의 삭제, 수정, 조회 등 관리를 할 수 있도록 하는 
    서비스
---

![width:500 bg right:55%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/PN_Nova.png)

# Nova / Placement

---

![width:500 bg right:45%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Nova_Structure.png)

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

---

# Request Flow when Launching an Instance

---

### Request Flow when Launching an Instance

![width:8540px](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Request_Flow_Diagram.png)

---

### Transformation of CLI Request to Running Instances

![bg right width:600px](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Nova_Request_Flow.png)

---

### Network Connections between Compute Nodes and Instances

![bg right width:600px](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Neutron_Request_Flow.png)

---

### Other Interactions between the New Instance and Components in OpenStack

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
