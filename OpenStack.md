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
        
        There are two networking options; provider network and self-service network. Provider networks lack support for self-service (private) networks, layer-3 (routing) services, and advanced services such as LBaaS [^1] and FWaaS [^2]. For future developments, it is necessary to use provider networks. Further explanations are in ['Neutron'](#Neutron) under OpenStack Services Types and Brief Definition.

[//]: # (Successfuly uploaded image)

---

### 2. OpenStack Services Types and Brief Definition
There are various kinds of services in OpenStack. As a minimum, the following services are essential when you launch an OpenStack project.
* Keystone

[//]: # (Keystone is an identity service.)
* Glance

[//]: # (Glance is an image service.)
* Placement

* Nova

[//]: # (Nova is a compute service.)
* # Neutron

[//]: # (Neutron is a networking service.)
* Cinder[^3]

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

