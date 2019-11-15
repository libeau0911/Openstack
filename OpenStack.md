OpenStack
=====
Contents
--------
1. Definition and Architecture
    * Definition
    * Architecture
2. OpenStack Services Types and Brief Definition
    * Keystone
    * Glance    
    * Placement
    * Nova  
    * Neutron
    * Cinder
3. Request Flow for Launching an Instance in OpenStack

---

### 1. Definition and Architecture
* Definition
    The OpenStack Project is an open source cloud computing platform that supports all types of cloud environments.
* Architecture
    - Conceptual Architecture   
     The below diagram shows the relationships among the OpenStack services.
    ![Conceptual Architecture](/Conceptual_Architecture.png) 

[//]: # (Successfuly uploaded image)

---

### 2. OpenStack Services Types and Brief Definition
There are various kinds of services in OpenStack. As a minimum, the following services are essential when you launch an OpenStack project.
* Keystone
    Keystone is an identity service.
* Glance
    Glance is an image service.
* Placement
* Nova
    Nova is a compute service.
* Neutron
    Neutron is a networking service.
* Cinder<sup>1</sup>
    Cinder is a block storage service.
---

### 3. Request Flow for Launching an Instance in OpenStack

Below is the diagram that shows the request flow when launching an instance in OpenStack.
![Request Flow for Launching Instance](/Request_Flow_Diagram.PNG)

The diagram can be split into two big blocks; transformation of CLI request to running instances (Nova), network connections between compute nodes and instances (Neutron).





<sup>1</sup>: Cinder is not essential when launching an instance, but this service is explained for it will be used in future developments. 
    
