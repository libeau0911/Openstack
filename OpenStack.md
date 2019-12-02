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

---

### OpenStack Trend & Structure

![OpenStack(AWS) Structure](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Openstack_Structure_AWS.png)

---

### OpenStack Trend & Structure

#### Network Structure

![width:9400px](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Network_Architecture.png)

---

# OpenStack Features

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

![width:500 bg right:46%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Glance_Structure.png)

## Glance

- **오픈스택의 이미지 관리 서비스**
    사용자들이 VM 이미지의 삭제, 수정, 조회 등 관리를 할 수 있도록 하는 
    서비스

---

![width:500 bg right:45%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Nova_Structure.png)

## Nova

- **오픈스택의 컴퓨팅 서비스**
    클라우드 컴퓨팅 시스템을 호스팅하고 관리

### Placement

- 리소스 프로바이더에 대한 인벤토리와 사용 정보를 추적하는 데 사용

---

![width:500 bg right:45%](https://raw.githubusercontent.com/libeau0911/Openstack/master/images/Provider_Network.png)

## Neutron

- **오픈스택의 네트워킹 서비스**
    다른 오픈스택 서비스로 관리되는 인터페이스 장치를 생성하여 네트워크에 연결할 수 있도록 하는 서비스
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

# OpenStack Demo

