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


