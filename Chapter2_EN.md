# Chapter 2
## Cloud Computing Infrastructure and Core Technologies
### Concept of Cloud Computing Infrastructure
IaaS (Infrastructure as a Service) is a type of service provided by cloud computing providers, mainly referring to cloud service products related to infrastructure resources. This typically includes virtualized computing, virtualized storage, and virtualized network resources, along with supporting operating system images, system maintenance, and data backup. IaaS generally provides users with access to IT resources in a virtualized environment through the Internet. With IaaS, enterprises can build their own IT platforms on virtualized resources without maintaining various hardware resources themselves.

![Image1](https://github.com/user-attachments/assets/5cea61dc-7589-4236-a945-e3615df2d9cc)

The overall architecture of IaaS cloud computing is divided into several layers:
&nbsp;&nbsp;&nbsp;&nbsp;**Hardware Resources**: Mainly includes servers, storage devices, and network devices that construct data centers. Data centers usually have regional attributes, called Regions, and multiple AZs (Availability Zones) can be divided within a data center.
&nbsp;&nbsp;&nbsp;&nbsp;**Resource Pool**: Refers to the pools of virtual computing, virtual storage, and virtual network resources built on physical hardware resources. Resource pooling is the foundation for providing elasticity at the service layer.
&nbsp;&nbsp;&nbsp;&nbsp;**Cloud Services**: The interface through which users manage and use IaaS resources, critical for achieving "self-service" in cloud computing.
&nbsp;&nbsp;&nbsp;&nbsp;**Management Domain**: Primarily oriented towards IaaS cloud platform operators. At the operational level, it mainly provides unified operational capabilities for cloud services; at the maintenance level, it mainly provides unified maintenance capabilities for virtual and physical resources.
&nbsp;&nbsp;&nbsp;&nbsp;**Industry Applications**: Industry users can build business systems based on various cloud services to meet industry application needs.

### Core Technologies of Traditional Cloud Computing Infrastructure
#### Compute Virtualization
#### Storage Virtualization
In today's era of explosive data growth, both individuals and enterprises face data storage challenges. As a basic service of cloud computing IaaS infrastructure, cloud storage meets users' demands for using storage resources on demand, without worrying about the location of storage devices or how the storage system is constructed.

&nbsp;&nbsp;&nbsp;&nbsp;**Characteristics of Cloud Storage**: Massive storage, elastic scaling, high reliability, high performance, high availability.
&nbsp;&nbsp;&nbsp;&nbsp;**Categories of Cloud Storage**: Block storage, object storage, file storage.
##### Cloud Disk (Block Storage)
**Concept of Cloud Disk**:
&nbsp;&nbsp;&nbsp;&nbsp;A cloud disk is a virtual block storage service that provides low-latency, persistent, and highly reliable block-level random storage capabilities for virtual machines. When a virtual machine requires more disks, it can request cloud disks from the block storage service and attach them to the virtual machine. The usage of cloud disks is identical to that of traditional server physical disks.

**Characteristics of Cloud Disk**:
&nbsp;&nbsp;&nbsp;&nbsp;The backend of cloud disks usually employs a distributed storage system. Thus, compared to traditional server disks, cloud disks offer higher data reliability, higher I/O throughput, and more convenient usage. Cloud disks are suitable for databases, file systems, and other system software or applications that require block storage devices.
![Image2](https://github.com/user-attachments/assets/fad4cfd2-64a6-4fd9-b745-755f828279dc)
##### Object Storage
Object Storage Service (OBS) is a mass data storage service based on objects, providing customers with massive, secure, highly reliable, and low-cost data storage capabilities. Unlike the I/O read and write methods of block storage and file storage, object storage offers Restful API interfaces for users to create, modify, delete buckets, and upload, download, delete objects. Common online storage services can be considered a form of object storage. Object storage is generally suitable for low-frequency access or data archiving.

*Tips:  
Users access object storage through the network, performing object storage operations. This is the biggest difference compared to local operations with block or file storage.  
Buckets are storage spaces for objects in OBS. Object storage provides a flat storage method based on buckets and objects, eliminating the multi-level hierarchical directory structure of file systems.  
Objects are the basic units of data storage in OBS. An object is a collection of file data and its related attribute information (metadata). Data uploaded to OBS (pictures, videos, documents, etc.) are stored in the form of objects within buckets in OBS.*
![Image3](https://github.com/user-attachments/assets/54603ecb-6014-4c27-bbe9-6afd9affccf3)

##### Elastic File Storage
Elastic file service provides users' virtual machines with a fully managed shared file storage system, accessible using standard file access protocols (NFS and CIFS).

**Characteristics of Elastic File Service**:
&nbsp;&nbsp;&nbsp;&nbsp;The file system provided by the elastic file service can elastically scale, with a maximum capacity potentially reaching PB-level, and it also offers scalable performance to support massive data and high-bandwidth applications.
![Image4](https://github.com/user-attachments/assets/e941d9c9-682b-4813-afd0-2f95312d71fc)

##### Summary
| Type of Cloud Storage | Concept | Application Scenarios | Description |
|:----:|:---|:-----|:-----|
| Cloud Disk | Elastic block storage device, appearing as a virtual machine disk | Compared to traditional disks, it offers higher data reliability, higher I/O throughput, and easier use, suitable for file systems, databases, or other system software or applications requiring block storage devices. | Users can format, create file systems, etc., on cloud disks mounted to servers just like traditional server disks.<br>Shared cloud disks can be mounted to multiple elastic cloud servers simultaneously for data sharing.<br>Data access must occur within the data center's internal network. |
| File Storage | Provides users direct file system access interfaces, just like using local XFS, EXT4 file systems, supporting shared access among multiple virtual machines | Combines the high-speed direct access of cloud disks with the distributed sharing characteristics of elastic file services, suitable for storing documents, pictures, videos, and other unstructured data as a cloud storage service. | Complies with standard file protocols and can be mounted to servers, providing direct file system access interfaces like using local file directories.<br>Data sharing, multiple servers can mount the same file system, allowing shared operations and access.<br>Data access must occur within the data center's internal network. |
| Object Storage | Mass storage based on objects, users upload or download object files through API or SDK | Suitable for video cloud scenarios, providing file storage for high-bandwidth, mass data scenarios. | Users must access object storage through programming or third-party tools.<br>Data sharing. Servers, embedded devices, IoT devices, all users call the same path, and can access shared object storage data.<br>Data access is allowed in the public network, meeting Internet application needs. |

#### Network Virtualization
##### Overview of Cloud Network
A computer network is a digital telecommunications network that allows nodes to share resources. In a network, computer devices exchange data through data links between nodes. The emergence of cloud computing has driven the birth of cloud networks, and with the advancement of cloud computing, cloud networks themselves are also evolving. Overall, cloud networks have the following characteristics.

&nbsp;&nbsp;&nbsp;&nbsp;**Resource Sharing**: For cloud networks, resource sharing mainly refers to the sharing of underlying network hardware resources by multiple tenants. To achieve resource sharing, cloud networks must have virtualization and security isolation capabilities. Currently, the common solution is to use Overlay technology based on VxLAN, where an additional tenant identifier layer is added on top of user data packet addressing, achieving network virtualization and isolation through "IP+UDP+VxLAN tenant identifier+user data packet".  
&nbsp;&nbsp;&nbsp;&nbsp;**Elastic Scaling**: Traditional physical hardware-based networking does not have elastic scaling capabilities. To enhance forwarding capabilities, more devices need to be added. To meet elastic scaling demands, cloud networks use clusters for scaling and provide elastic network capabilities for each user through network virtualization technology.  
&nbsp;&nbsp;&nbsp;&nbsp;**Self-Service**: This is the biggest difference between cloud networks and traditional networks. Traditional networks typically involve human-machine interfaces, where professional network administrators configure network devices via command lines. In contrast, cloud networks involve machine-machine interfaces with centralized management, allowing users to configure networks through control consoles.  
&nbsp;&nbsp;&nbsp;&nbsp;**Pay-As-You-Go**: Cloud networks support different billing methods based on bandwidth usage, traffic usage, etc. Cloud networks can bill each tenant's processing capacity and forwarding traffic at regular intervals.

##### Basic Capabilities of Cloud Network
Virtual Private Cloud (VPC) is the fundamental capability of cloud networks. VPC provides tenants with a logically isolated virtual network environment for cloud servers (including virtual machines and bare metal servers) that is self-configurable and manageable by the user. In a shared resource environment, the VPC network model offers basic security guarantees for user resources while simplifying network deployment for users.

In the VPC model, users can implement various network capabilities:
&nbsp;&nbsp;&nbsp;&nbsp;**Subnet**: In a VPC, users can plan and create multiple subnet segments to join different business virtual machines to different networks.
&nbsp;&nbsp;&nbsp;&nbsp;**Security Group**: Security groups can divide cloud hosts into different security domains and set different access rules for each security domain.
&nbsp;&nbsp;&nbsp;&nbsp;**Virtual Router**: Different subnets in the same VPC can communicate through virtual routers, allowing cross-network segment host communication.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Virtual Private Gateway (VPG)**: Provides a gateway for connecting to the internet or other networks, enabling cross-cloud or cross-data center connectivity.
&nbsp;&nbsp;&nbsp;&nbsp;**Elastic IP**: Offers public IP addresses that can be dynamically assigned to instances, allowing external access to the internet.

![Image5](https://github.com/user-attachments/assets/99fa7d63-4913-4e64-84c8-1f568a2c9a21)

#### Application Examples of Core Cloud Network Technologies
**Case Study: Cloud Network for E-commerce Platform**:
An e-commerce platform requires a highly elastic and scalable network infrastructure to handle sudden spikes in traffic during sales events. The platform uses the following cloud network components:
&nbsp;&nbsp;&nbsp;&nbsp;1. **VPC**: Creates isolated virtual networks for different services (e.g., front-end, back-end, database).
&nbsp;&nbsp;&nbsp;&nbsp;2. **Subnets**: Segregates the network into smaller, manageable sections.
&nbsp;&nbsp;&nbsp;&nbsp;3. **Security Groups**: Defines security rules for different instances to control traffic.
&nbsp;&nbsp;&nbsp;&nbsp;4. **Elastic IPs**: Assigns public IPs to front-end servers for internet access.
&nbsp;&nbsp;&nbsp;&nbsp;5. **Load Balancers**: Distributes incoming traffic across multiple instances to ensure high availability and fault tolerance.

By leveraging these cloud network components, the e-commerce platform can quickly adapt to varying traffic loads, ensuring a seamless shopping experience for users.

#### Conclusion
Cloud computing infrastructure and core technologies are fundamental to modern IT operations. Understanding the concepts and capabilities of IaaS, including compute virtualization, storage virtualization, and network virtualization, is crucial for building scalable, reliable, and efficient cloud-based systems. Cloud storage solutions, such as cloud disks, object storage, and elastic file storage, provide diverse options for different storage needs. Cloud networks offer essential services like VPC, subnets, security groups, and elastic IPs, enabling flexible and secure network configurations. As cloud computing continues to evolve, staying informed about the latest advancements and best practices is essential for leveraging its full potential.
