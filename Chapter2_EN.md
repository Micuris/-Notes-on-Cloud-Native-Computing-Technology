# Chapter 2
## Cloud Computing Infrastructure and Core Technologies
### Concept of Cloud Computing Infrastructure
IaaS is a service provided by cloud computing service providers. It mainly refers to cloud service products related to infrastructure resources, typically including virtualized computing, virtualized storage, virtualized networks, and supporting content such as operating system images, system maintenance, and data backups. IaaS generally provides access to IT resources in a virtualized environment over the Internet. Through IaaS, enterprises can build their IT platforms on virtualized resources without needing to maintain various hardware resources themselves.

![Image1](https://github.com/user-attachments/assets/5cea61dc-7589-4236-a945-e3615df2d9cc)

From the overall architecture perspective, IaaS cloud computing mainly consists of the following levels:
- Hardware Resources: These include servers, storage devices, and network devices that make up data centers. Data centers generally have regional attributes, called Regions, which can be divided into multiple Availability Zones (AZs) within a region.
- Resource Pool: This refers to virtual computing, virtual storage, and virtual network resource pools built on physical hardware resources. Resource pooling is the foundation for providing elasticity at the service layer.
- Cloud Services: Cloud services are the interfaces through which users manage and use IaaS resources, and are key to achieving the "self-service" aspect of cloud computing.
- Management Domain: This is mainly for IaaS cloud platform operators. The operations layer provides unified operational capabilities for cloud services, while the maintenance layer offers unified maintenance capabilities for virtual and physical resources.
- Industry Applications: Industry users can build business systems based on various cloud services to meet the needs of industry applications.

### Core Technologies of Traditional Cloud Computing Infrastructure
#### Computing Virtualization
#### Storage Virtualization
Today is an era of explosive data growth, where both individuals and enterprises face data storage issues. As a basic service of cloud computing IaaS infrastructure, cloud storage meets the demand for users to use storage resources on demand without worrying about where the storage devices are or how the storage system is constructed.

Characteristics of Cloud Storage:
- Massive storage
- Elastic scalability
- High reliability
- High performance
- High availability

Types of Cloud Storage:
- Block Storage
- Object Storage
- File Storage

##### Cloud Disk (Block Storage)
The concept of Cloud Disk:
- Cloud Disk is a virtual block storage service that provides low latency, persistent, high-reliability, and random data block-level storage capabilities for virtual machines. When a virtual machine needs more disks, it can request cloud disks from the block storage service and attach them to the virtual machine. The use of cloud disks is identical to that of traditional server physical disks.

Characteristics of Cloud Disk:
- The backend of cloud disks is usually a distributed storage system, which provides higher data reliability, higher IO throughput, and more convenient usage compared to traditional server disks. Cloud disks are suitable for databases, file systems, and other system software or applications that require block storage devices.

![Image2](https://github.com/user-attachments/assets/fad4cfd2-64a6-4fd9-b745-755f828279dc)

##### Object Storage
Object Storage Service (OBS) is a massive data storage service based on objects, providing customers with massive, secure, highly reliable, and low-cost data storage capabilities. Unlike block storage and file storage, object storage provides RESTful API interfaces for creating, modifying, deleting buckets, and uploading, downloading, and deleting objects. Common network disks can often be considered a form of object storage. Object storage is generally used for infrequent access or data archiving.

*Tips:
Users access object storage over the network to perform object retrieval operations, which is the main difference from local operations of block or file storage.
A bucket is the storage space for objects in OBS. Object storage offers a flat storage structure based on buckets and objects, eliminating the multi-level hierarchical directory structure of file systems.
An object is the basic unit of data storage in OBS. An object is a collection of a file's data and its related attribute information (metadata). Data uploaded to OBS (images, videos, documents, etc.) are stored in buckets in OBS as objects.*

![Image3](https://github.com/user-attachments/assets/54603ecb-6014-4c27-bbe9-6afd9affccf3)

##### Elastic File Storage
Elastic File Service provides users with a fully managed shared file storage system, accessible from virtual machines using standard file access protocols (NFS and CIFS).

Characteristics of Elastic File Service:
- The file system provided by Elastic File Service can scale elastically, with a maximum capacity reaching PB-level, and it also features scalable performance, providing robust support for massive data and high-bandwidth applications.

![Image4](https://github.com/user-attachments/assets/e941d9c9-682b-4813-afd0-2f95312d71fc)

##### Summary

| Cloud Storage Type | Concept | Application Scenarios | Description |
|:----:|:---|:-----|:-----|
| Cloud Disk | Extensible block storage device, appearing as virtual machine disks | Compared to traditional disks, it offers higher data reliability, higher I/O throughput, and more straightforward usability, suitable for file systems, databases, or other system software or applications requiring block storage devices. | Like using traditional server disks, users can format the cloud disks attached to servers, create file systems, etc.<br> Shared cloud disks can be attached to multiple elastic cloud servers simultaneously, enabling data sharing.<br> Data access must occur within the data center's internal network. |
| File Storage | Provides users with direct file system access interfaces, allowing them to use the file storage system like local XFS or EXT4 | Combines the high-speed direct disk access features of cloud disks with the distributed sharing characteristics of elastic file services, suitable for storing documents, images, audio, and video data. | Conforms to standard file protocols, can mount file services to servers, providing direct file system access interfaces like local file directories.<br> Data sharing, multiple servers can mount the same file system, allowing shared data operations and access.<br> Data access must occur within the data center's internal network. |
| Object Storage | Massive storage based on objects, users upload or download object files via API or SDK | Suitable for video cloud scenarios, providing file storage for high-bandwidth, massive data scenarios. | Users must access object storage via programming or third-party tools.<br> Data sharing. Servers, embedded devices, IoT devices, all users can access shared object storage data via the same path.<br> Data access is allowed on the public network, meeting internet application needs. |

### Network Virtualization
#### Overview of Cloud Networks
A computer network, commonly referred to simply as a network, is a digital telecommunications network that allows nodes to share resources. In a network, computer devices exchange data through data links between nodes. The advent of cloud computing has driven the development of cloud networks, and as cloud computing advances, cloud networks themselves continue to evolve. Overall, cloud networks exhibit the following characteristics:

- **Resource Sharing**: In the context of cloud networks, resource sharing primarily refers to multiple tenants sharing the underlying network hardware resources. To achieve resource sharing, cloud networks must possess virtualization and security isolation capabilities. Currently, an Overlay technology scheme based on VxLAN is commonly used. This involves adding a layer of tenant identification on top of user data packets, achieving network virtualization and isolation through "IP+UDP+VxLAN user ID+user data packet."
- **Elastic Scalability**: Traditional physical hardware-based physical networking lacks elastic scalability; enhancing forwarding capacity requires adding more devices. To meet the demands for elastic scalability, cloud networks adopt a cluster approach for extension and use network virtualization technology to provide elastic network capabilities for each user.
- **Self-Service**: This is the most significant difference between cloud networks and traditional networks. Traditional networks typically involve human-to-machine interfaces, where professional network administrators configure network devices through command lines. In contrast, cloud networks feature machine-to-machine interfaces and centralized management, enabling users to configure networks through a control panel.
- **Pay-As-You-Go**: Cloud networks support various billing methods, such as bandwidth usage and traffic usage. They possess the capability to measure processing capacity and forwarding traffic for each tenant for billing purposes.

#### Basic Capabilities of Cloud Networks
Virtual Private Cloud (VPC) is the fundamental capability of cloud networks. VPC provides tenants with a logically isolated virtual network environment for cloud servers (including virtual machines and bare-metal servers) that users can configure and manage independently. In a cloud computing shared resource scenario, the VPC network model offers basic security guarantees for user resources while simplifying network deployment.

Within the VPC model, users can implement various network capabilities:
- **Subnet**: Within a VPC, users can plan and create multiple subnet segments, allowing different business virtual machines to join different networks.
- **Security Group**: Security groups allow cloud hosts to be divided into different security domains, with each domain having different access rules.
- **Virtual Router**: Different subnets within the same VPC can be connected via a virtual router, enabling communication across subnet segments.
- **NAT Gateway**: The SNAT function of the NAT gateway enables tenant virtual machines to access the public network.
- **Elastic Public IP**: If users want to access applications on virtual machines from the public network, they can bind an elastic public IP to the virtual machine. Internet users can access the virtual machine through the bound public IP.

![Image 5](https://github.com/user-attachments/assets/435b93ce-020c-4890-8cd1-9b89c7649c75)

#### Advanced Capabilities of Cloud Networks
Cloud networks also provide advanced network engineering features such as load balancing, firewalls, VPN access, and dedicated line access, as described below:
![image](https://github.com/user-attachments/assets/c9c875c9-32e6-4eaa-b4e3-95147e7b6464)

#### Key Technologies in Cloud Networks
##### VxLAN
**Overlay Network**: An overlay network is a virtual network built on top of another computer network, known as the underlay network. Overlay networks rely heavily on VxLAN technology in cloud networks because VxLAN addresses three critical issues faced by cloud computing networks:

1. **Scale Limitations of Traditional Network Isolation Technology**: Traditional VLANs can only establish 4096 virtual networks, insufficient for the needs of public clouds and large-scale virtualization clusters. In contrast, VxLAN uses a 24-bit VNI to identify different Layer 2 segments, theoretically supporting up to 16,777,216 LANs.
2. **Maintaining VM IP Addresses During Migration**: In cloud computing, virtual machine migration is common. To ensure uninterrupted service, the VM's IP address must remain unchanged during migration. Overlay technology implements a Layer 2 network on top of the traditional network layer, allowing VMs to remain within the virtual network created by the overlay after migration, thus keeping their IP addresses unchanged.
3. **Handling Large VM Scales**: A single cluster can have a vast number of VMs, causing significant pressure on network devices due to the large number of MAC addresses and ARP requests. In an overlay network built with VxLAN, network packets sent by VMs are encapsulated into IP packets. This means the network only needs to know the MAC addresses of different VTEPs, reducing the MAC table entries from hundreds of thousands to a few thousand. ARP requests are also confined to VETP clusters, effectively reducing network pressure caused by large VM scales.

##### VxLAN Encapsulation and Packet Format
VxLAN defines a MAC-in-UDP encapsulation format, as shown in the figure below. A VXLAN header is added before the original Layer 2 network packet, which is then placed into a UDP and IP packet. Through MAC-in-UDP encapsulation, VxLAN establishes a Layer 2 tunnel over a Layer 3 network. VxLAN introduces an 8-byte VxLAN header, with 24 bits allocated for the VNI. The VxLAN and original Layer 2 frame are encapsulated into a UDP packet. The 24-bit VNI identifies different Layer 2 segments, supporting up to 16,777,216 LANs.
![image](https://github.com/user-attachments/assets/d143381d-6486-4cd8-ab42-da791e37083f)

##### VxLAN Tunnel Endpoint and Packet Forwarding Process
VxLAN uses VxLAN Tunnel Endpoint (VTEP) devices to handle VxLAN encapsulation and decapsulation. Each VTEP has an IP interface configured with an IP address. The VTEP uses this IP to encapsulate Layer 2 frames and transmit and receive the encapsulated VxLAN packets through the IP interface. The VxLAN network and the underlying IP network between two VTEPs are independent of each other. VxLAN packets are routed based on the outer IP header, which uses the IP addresses of the source and destination VTEPs.
![image](https://github.com/user-attachments/assets/771dc241-48c6-462a-a31a-57ce42018118)

##### OpenvSwitch (OVS)
OpenvSwitch, abbreviated as OVS, is a high-quality, multilayer virtual switch software designed to support large-scale network automation through programmability. It also supports standard management interfaces and protocols. OVS is mainly used in virtual machine (VM) environments, serving as a virtual switch that supports various virtualization technologies such as Xen/XenServer, KVM, and VirtualBox. In these virtualized environments, the virtual switch primarily has two functions: facilitating traffic between virtual machines and enabling communication between virtual machines and external networks.

##### The Role of OVS in Cloud Networks
OVS can implement various network functions through OpenFlow flow tables and, using the OpenFlow protocol, can easily achieve the separation of control and forwarding in a cloud network SDN (Software-Defined Networking) solution. Based on OVS, data centers can benefit from highly flexible network configuration capabilities.
![image](https://github.com/user-attachments/assets/d6d77630-6077-4f42-b479-0793db563aaa)

##### OVS Architecture
![image](https://github.com/user-attachments/assets/56dd0e74-d8f0-4bdb-b633-b315c815c418)
- **ovs-vswitchd**: The main module, implementing the switch daemon.
- **openvswitch.ko**: A Linux kernel module that supports data flow switching within the kernel.
- **ovsdb-server**: A lightweight database server that stores configuration information. ovs-vswitchd retrieves configuration information from this database.
- **ovs-dpctl**: Used to configure the switch kernel module.
- **ovs-vsctl**: Queries and updates the configuration of ovs-vswitchd.
- **ovs-appctl**: Sends command messages to run the relevant daemon.
- **ovs-ofctl**: Queries and controls OpenFlow switches and controllers.

#### Basic Resource Management
##### Service-Oriented Architecture of OpenStack
The service-oriented architecture of OpenStack is illustrated in the following diagram:
![image](https://github.com/user-attachments/assets/36de3e66-5b6e-4b7e-8083-7b66a5a0f26b)

OpenStack is composed of multiple independent services, each represented by a separate box. Each service exposes a RESTful API interface for external interaction, and services communicate with each other over HTTP. Authentication and access control are managed centrally by the identity service.

###### Key Services Include:
- **Dashboard-Horizon**: Provides a graphical user interface for operations.
- **Compute Service-Nova**: Handles CRUD (Create, Read, Update, Delete) operations for virtual machines.
- **Image Service-Glance**: Manages virtual machine images, including storage, retrieval, pulling, and cloning.
- **Network Service-Neutron**: Manages network resources, including networks, subnets, ports, security group rules, routers, firewalls, and load balancing.
- **Block Storage Service-Cinder**: Provides block storage services, with backends such as Ceph and LVM.
- **Object Storage Service-Swift**: Offers object storage services, compatible with AWS S3 interface.
- **Identity Service-Keystone**: Handles authentication and access control for inter-service communication.

##### Communication Mechanism within the Same Service in OpenStack
Within a service, components communicate through RPC (Remote Procedure Call) rather than RESTful API calls. OpenStack uses message middleware (Queue) to implement asynchronous RPC calls. The following diagram illustrates the internal RPC communication mechanism within the Nova service:
![image](https://github.com/user-attachments/assets/6dd258de-db5f-4537-8463-8677231959d1)

###### Example of Nova Service Internal Virtual Machine Creation Call Flow:
1. **nova-api** component exposes RESTful API interfaces and receives virtual machine creation requests.
2. **nova-api** makes an RPC call to **nova-conductor**, implemented by writing the request to a message queue.
3. **nova-conductor** retrieves the request from the message queue and makes an RPC call to **nova-scheduler**, also by writing the request to the message queue.
4. **nova-scheduler** selects a suitable compute node for the virtual machine and calls the **nova-compute** service, again by writing the request to the message queue.
5. **nova-compute** retrieves the request from the message queue and interacts with the hypervisor and other services (e.g., image, network, storage) to create the virtual machine.

##### OpenStack Virtual Machine Creation Signaling Process
The signaling process for creating a virtual machine in OpenStack is illustrated in the following diagram. It consists of inter-service and intra-service calls involving five main services: authentication service, compute service, image service, network service, and block storage service. The process is broken down into six main operations: 1) Authentication and Authorization; 2) Compute Node Scheduling; 3) Image Retrieval; 4) Network Resource Allocation; 5) Storage Resource Allocation; and 6) Configuring and Creating the Virtual Machine.
![image](https://github.com/user-attachments/assets/460ac463-0fc5-473a-a5ff-fe9ccbe96a33)

###### Six Main Operations for Virtual Machine Creation:
**1. Inter-service Authentication and Authorization**
   - **Steps 1, 2:** The client logs in and retrieves a token.
   - **Steps 3, 4, 5:** The client calls the compute service, and Nova performs authentication and authorization.
   - **Steps 21, 24, 27:** Nova-compute performs authentication and authorization when calling the image, network, and block storage services, respectively.

**2. Compute Node Scheduling (Intra-service Interaction within Compute Service)**
   - **Steps 6 to 19:** These steps represent the process of selecting a suitable compute node for the virtual machine.

**3. Image Retrieval**
   - **Steps 20, 21:** Requests are made to the image service to pull the required image.

**4. Network Resource Allocation**
   - **Steps 23, 25:** Requests are made to the network service to allocate network resources.

**5. Storage Resource Allocation**
   - **Steps 26, 28:** Requests are made to the block storage service to allocate storage resources.

**6. Configuring and Creating the Virtual Machine**
   - **Step 29:** Based on the allocated resources, the virtual machine is configured and created.

### Intelligent Operations and Maintenance (Ops)
#### Basic Concepts of Operations and Maintenance (Ops)
- **Definition:** Operations and maintenance refer to the process of managing and maintaining online services or products through a series of steps and methods.
- **Objects:** Data centers, networks, storage, physical machines, virtual machines, and infrastructure, including databases, middleware platforms, and big data platforms.
- **Responsibilities:** Ensuring system stability throughout the product/service lifecycle.

| Stage | Operations Responsibilities |
|:----:|:--------|
| Design Phase | Stability assessment: Evaluating the rationality of system architecture design, including the presence of single points of failure and fault tolerance, ensuring basic elements for stable operation. <br> Resource evaluation: Assessing required server resources, network resources, and their distribution, ensuring reasonable resource applications and controlling resource usage costs. |
| Development Phase | Environment deployment, dependency library and package management, operating system maintenance, database preparation, etc. |
| Testing Phase | Deployment of the testing environment, stability assessment |
| Deployment Phase | Automated deployment, stability inspection, scalable deployment, etc. |
| Online Operation Phase | Ensuring stable online service operation: <br> Real-time monitoring: Monitoring service operation status in real-time, identifying anomalies and resource consumption, generating regular reports, evaluating overall service operation, and identifying potential issues.<br> Fault handling: Timely addressing any anomalies to prevent escalation or service interruption. <br> Capacity management: Planning and implementing resource evaluation, expansion, data center migration, and traffic scheduling as the service scales. |
| Decommissioning/Rollback Phase | Halting services and ensuring resource recovery |

#### Development Stages of Operations
##### Manual Stage
- **Content:** Responsible for server selection, software and hardware initialization, service deployment and decommissioning, configuration monitoring, and viewing monitoring data.
- **Characteristics:** Few servers and simple business needs meant that a small number of operations engineers could complete the tasks without being a bottleneck for normal business operations. There were no standardized processes, and the quality of operations could not be evaluated.

##### Tool-based Stage
- **Background:** As the industry evolved, business systems became more complex, making it impossible to rely solely on manual operations.
- **Content:** Automating parts of the operations processes and repetitive tasks through scripting.
- **Characteristics:** Simplifying operational workflows, enhancing efficiency, and reducing the likelihood of errors.

##### Platform-based Stage
- **Background:** Scripts and tools were scattered and difficult to manage, and still required manual intervention. As business complexity increased, managing a large number of scripts became inefficient and complicated.
- **Content:** Integrating automated scripts and tools to build more user-friendly and efficient operations management tools at the system level, including monitoring, alerting, and automation platforms.
- **Characteristics:** Enhancing development and testing efficiency, reducing operational costs, minimizing system risk, and improving system availability.

##### Intelligent Ops Stage
- **Background:** Despite advancements in operations management technology, emergency operations like anomaly detection and fault diagnosis still required manual intervention.
- **Content:** Leveraging machine learning and data science to analyze and process operational data from services and devices, enabling automatic issue detection and resolution.
- **Characteristics:** Significantly improving operational efficiency; infrastructure resources dynamically adapt to business needs, achieving closed-loop management and ultimately "automatic driving" for infrastructure operations.

#### Challenges in Ops
- **Heterogeneous Resource Composition:** Adapting and managing multi-vendor heterogeneous hardware resources, and ensuring compatibility between new and old equipment and software systems.
- **Higher Efficiency Requirements:** Under DevOps, the efficiency of planning, development, testing, and delivery is increasingly demanded. Issues need to be resolved swiftly.
- **Massive Data Processing:** With business growth, the scale of cloud resource pools increases, generating vast amounts of operational data, complicating data collection, processing, and analysis. Multiple sampling types, inconsistent data formats, and non-standardized collection metrics make it difficult to build operational models.
- **Increased System Complexity:** Transitioning from integrated to layered models, and then to service-oriented models, has made system architecture more complex. More dependencies on virtual machines, middleware, and container runtimes make problem location and resolution more challenging.
