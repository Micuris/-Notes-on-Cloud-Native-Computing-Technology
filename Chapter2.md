## 云计算基础设施及核心技术
### 云计算基础设施的概念
IaaS是云计算服务商提供的一种服务，它主要是指基础设施资源相关的云服务产品，通常主要指虚拟化计算、虚拟化存储、虚拟化网络等基础资源，以及配套的操作系统镜像、系统维护、数据备份等内容。IaaS一般是通过互联网向用户提供对虚拟化环境中IT资源的访问，通过IaaS，企业就可以在虚拟化资源上构建自己的IT平台，而不需要自己维护各种各样的硬件资源。

![图片1](https://github.com/user-attachments/assets/5cea61dc-7589-4236-a945-e3615df2d9cc)

IaaS云计算从整体架构上主要分为如下几个层面：  
&emsp;&emsp;硬件资源：主要包括构建数据中心的服务器、存储设备、网络设备。数据中心一般具有地域属性，称为Region，在数据中心内又可以划分多个AZ。  
&emsp;&emsp;资源池：是指基于物理硬件资源构建的虚拟计算、虚拟存储、虚拟网络资源池，资源池化是在服务层提供弹性能力的基础。  
&emsp;&emsp;云服务：云服务是用户管理和使用IaaS资源的界面，是实现云计算“自助服务”的关键。  
&emsp;&emsp;管理域：主要面向IaaS云平台运营维护者，运营层面主要是针对云服务提供统一的运营能力；运维层面主要是针对虚拟资源和物理资源的统一运维能力。  
&emsp;&emsp;行业应用：行业用户可以基于各种云服务构建业务系统，满足行业应用需求

### 传统云计算基础设施核心技术
#### 计算虚拟化
#### 存储虚拟化
当今是一个数据爆炸式增长的时代，无论是个人、还是企业都面临数据存储的问题。云存储作为云计算IaaS 基础设施的一种基本服务，满足了用户按需使用存储资源的诉求，而无需关心存储设备在何处、存储系统如何构建。
  
&emsp;&emsp;云存储特征：海量存储、弹性伸缩、高可靠、高性能、高可用性  
&emsp;&emsp;云存储分类：块存储、对象存储、文件存储
##### 云硬盘（块存储）
云硬盘的概念：  
&emsp;&emsp;云硬盘是一种虚拟块存储服务，该服务可以是为虚拟机提供的低时延、持久性、高可靠的数据块级随机存储能力，当虚拟机需要更多的硬盘时，可以向块存储服务申请云硬盘，并挂在给虚拟机，云硬盘的使用方式和传统服务器物理硬盘完全一致。  

云硬盘特点：  
&emsp;&emsp;云硬盘后端通常一般是是分布式存储系统，因此相比传统的服务器硬盘，云硬盘具有更高的数据可靠性、更高的IO吞吐能力和更加便捷的使用方式。云硬盘适用于数据库、文件系统等需要块存储设备的系统软件或应用。
![图片2](https://github.com/user-attachments/assets/fad4cfd2-64a6-4fd9-b745-755f828279dc)
##### 对象存储
对象存储服务（Object StorageService，OBS）是基于对象的海量数据存储服务，为客户提供海量、安全、高可靠、低成本的数据存储能力。与块存储、文件存储的IO读写的方式不同，对象存储向用户提供包括创建、修改、删除桶（bucket），上传、下载、删除对象的RestfulAPI接口。常见的网盘，通常就可以认为是一种对象存储。对象存储一般适用于低频访问或者进行数据归档时使用。  
  
*Tips：  
用户通过网络访问对象存储，执行对象的存取操作，这是与块或者文件存储本地操作的最大不同。  
桶是OBS中存储对象的存储空间,对象存储提供了基于桶和对象的扁平化存储方式，桶中的所有对象都处于同一逻辑层级，去除了文件系统中的多层级树形目录结构。  
对象是OBS中数据存储的基本单位，一个对象实际是一个文件的数据与其相关属性信息（元数据）的集合体。用户上传至OBS的数据（图片、视频、文档等）都以对象的形式保存在OBS的桶中。*
![图片3](https://github.com/user-attachments/assets/54603ecb-6014-4c27-bbe9-6afd9affccf3)

##### 弹性文件存储
弹性文件服务为用户虚拟机提供一个完全托管的共享文件存储系统，在虚拟机中可以基于标准的文件访问协议（NFS和CIFS）进行访问。  
弹性文件服务特点：  
&emsp;&emsp;弹性文件服务提供的文件系统能够弹性伸缩，最大容量甚至可以达到PB级规模，同时其也具备可扩展的性能，为海量数据、高带宽应用提供有力的支撑。
![图片4](https://github.com/user-attachments/assets/e941d9c9-682b-4813-afd0-2f95312d71fc)

##### 小结
|云存储类型|概念|应用场景|说明|
|:----:|:---|:-----|:-----|
|云硬盘|	可弹性扩展的块存储设备，表现为虚拟机磁盘|相比传统硬盘，具有更高的数据可靠性，更高的I/O吞吐能力和更加简单易用等特点，适用于文件系统、数据库或者其他需要块存储设备的系统软件或应用。|像使用传统服务器硬盘一样用户可以对挂载到服务器上的云硬盘做格式化、创建文件系统等操作。<br>共享云硬盘可以同时挂载给多台弹性云服务器，实现数据共享。<br>数据访问必须在数据中心内部网络中。|
|文件存储|向用户直接提供文件系统访问接口，就像使用本地的XFS、EXT4一样使用文件存储系统，支持多个虚拟机共享访问|兼具云硬盘高速直接访问磁盘的特点及弹性文件服务的分布式共享特点，是一种可存储文档、图片、影音视频等非结构化数据的云存储服务。|符合标准文件协议，可以将文件服务挂载给服务器，像向用户直接提供文件系统访问接口，使用本地文件目录一样。<br>数据共享,多台服务器可挂载相同的文件系统，数据可以共享操作和访问。<br>数据访问必须在数据中心内部网络中。|
|对象存储|基于对象的海量存储，用户通过API或者SDK进行上传或者下载对象文件。|适用于视频云场景，为高带宽、海量数据场景的应用提供文件存储。	|用户必须通过编程或第三方工具访问对象存储。<br>数据共享。服务器、嵌入式设备、IOT设备，所有用户调用相同路径，均可访问共享的对象存储数据。<br>数据访问允许在公网中，满足互联网应用需求。|

#### 网络虚拟化
##### 云网络概述
计算机网络（Computer Network），通常也简称网络，是指允许节点分享资源的数字电信网络。在网络中，电脑设备会透过节点之间的数据链路互相交换数据。云计算的出现推动了云网络的诞生，同时，随着云计算的推进，云网络本身也在不断发展变化，总体而言，云网络具备如下几个特征。

&emsp;&emsp;资源共享：对于云网络而言，资源共享主要是指多租户共享底层的网络硬件资源，为了实现资源共享，云网络就必须具备虚拟化与安全隔离能力。现在，通常使用基于VxLAN的Overlay技术方案，即在用户数据报文编址基础上再叠加一层租户标识，通过“IP+UDP+VxLAN用户标识+用户数据报文”实现网络虚拟化及隔离。  
&emsp;&emsp;弹性伸缩：传统基于物理硬件的物理组网不具备弹性伸缩能力，要增强转发能力只能添加更多设备。云网络为了应对弹性伸缩需求，在实现上采用集群的方式支持扩展，结合网络虚拟化技术为每个用户提供了弹性网络能力。  
&emsp;&emsp;自助服务：这是云网络和传统网络最大的不同，传统网络一般是人-机接口，由专业网管通过命令行对网络设备进行配置，但是云网络是机-机接口，集中管理，用户通过控制台就可以实现网络配置。  
&emsp;&emsp;按需付费：云网络支持用户按使用带宽、使用流量等不同的计费方式，云网络具备对每个租户的处理能力和转发流量进行定时打点计费的能力。  

##### 云网络基本能力
虚拟私有云（Virtual Private Cloud，VPC）是云网络的最基本能力，VPC向租户提供了一套为云服务器（包括虚拟机和裸机）构建的逻辑隔离的、由用户自主配置和管理的虚拟网络环境，在云计算共享资源场景下，VPC网络模型为用户资源提供了基本安全性保证，同时简化了用户的网络部署。

在VPC模型下，用户可以实现多种网络能力：  
&emsp;&emsp;子网：在一个VPC下，用户可以规划并创建多个子网网段，从而将不同业务的虚拟机加入不同的网络。  
&emsp;&emsp;安全组：通过安全组可以将云主机划分到不同的安全域，并为每个安全域设定不同的访问规则  
&emsp;&emsp;虚拟路由器：在同一VPC下的不同子网，可以通过虚拟路由器进行连通，实现跨网段主机的通信。  
&emsp;&emsp;NAT网关：租户的虚拟机可以通过NAT网关的SNAT功能实现公网访问。  
&emsp;&emsp;弹性公网IP：如果用户希望从公网访问虚拟机上的应用，可以给虚拟机绑定弹性公网IP，Internet用户	通过绑定的公网IP就可以访问虚拟机。  
![图片5](https://github.com/user-attachments/assets/435b93ce-020c-4890-8cd1-9b89c7649c75)

##### 云网络高级能力
云网络还提供负载均衡、防火墙、VPN接入、专线接入等高级网络工程，说明如下
![image](https://github.com/user-attachments/assets/c9c875c9-32e6-4eaa-b4e3-95147e7b6464)

##### 云网络关键技术
###### VxLAN
Overlay Network：Overlay 网络建立在另一个计算机网络之上的虚拟网络(不能独立出现)，Overlay 底层依赖的网络是 Underlay 网络。在云网络中大量使用基于VxLAN的Overlay网络技术，是因为VxLAN网络解决了云计算网络面临的三个关键问题：  

1. 传统网络隔离技术的规模限制：传统VLAN只能建立4096个虚拟网络，无法满足公有云及大规模虚拟化集群下更多虚拟网络的要求，而VxLAN有24-bit的VNI用于标识不同的二层网段，理论可以支持16777216个LAN。  
2. 虚拟机迁移IP不变：云计算中虚拟机的迁移比较常见，为了保证业务不中断，需要保证迁移过程中虚拟机IP地址不变，Overlay技术是在传统的网络层实现了二层网络，迁移后虚拟机仍然处于基于Overlay构建的虚拟网络中，不需要改变IP地址。  
3. 虚拟机规模问题：单个集群中虚拟机规模可能非常大，大量的MAC地址和ARP请求给网络设备带来巨大的压力，在使用VxLAN搭建的Overlay网络中，网络会将虚拟机发送的包重新封装成IP包，这样网络只需要知道不同VTEP的MAC地址，将MAC表项由几十万条降低至几千条，ARP请求也只会在集群的VETP之间扩散，有效降低虚拟机规模带来的网络压力。

###### VxLAN封包和包格式
VXLAN 定义了一个 MAC-in-UDP 的封装格式，具体封包格式如下图所示。
在原始的 Layer 2 网络包前加上 VXLAN header，然后放到 UDP 和 IP 包中。通过 MAC-in-UDP 封装，VXLAN 能够在 Layer 3 网络上建立起了一条 Layer 2 的隧道。VXLAN 引入了 8-byte VXLAN header，其中 VNI 占 24-bit。VXLAN 和原始的 L2 frame 被封装到 UDP 包中。这 24-bit 的 VNI 用于标示不同的二层网段，能够支持 16777216 个 LAN。
![image](https://github.com/user-attachments/assets/d143381d-6486-4cd8-ab42-da791e37083f)

###### VxLAN Tunnel Endpoint及包转发流程
VXLAN 使用 VXLAN tunnel endpoint (VTEP) 设备处理 VXLAN 的封装和解封。每个 VTEP 有一个 IP interface，配置了一个 IP 地址。VTEP 使用该 IP 封装 Layer 2 frame，并通过该 IP interface 传输和接收封装后的 VXLAN 数据包。VXLAN 网络与两个 VTEP 之间的底层 IP 网络相互独立。 VXLAN 数据包是根据外层的 IP header 路由的，该 header 将两端的 VTEP IP 作为源和目标 IP。
![image](https://github.com/user-attachments/assets/771dc241-48c6-462a-a31a-57ce42018118)

###### OpenvSwitch
OpenvSwitch简称OVS，它是一个高质量、多层的虚拟交换软件。它的目的是通过编程扩展支持大规模网络自动化，同时还支持标准的管理接口和协议。OpenvSwitch是一个虚拟交换软件，主要用于虚拟机VM环境，作为一个虚拟交换机，支持Xen/XenServer，KVM以及virtualBox多种虚拟化技术。在这种虚拟化的环境中，虚拟交换机主要有两个作用：传递虚拟机之间的流量，以及实现虚拟机和外界网络的通信。

###### OVS在云网络中的位置
OVS 通过openflow流表可以实现各种网络功能，并且通过openflow protocol可以方便的实现控制+转发分离的云网络SDN方案，基于OVS，可以为数据中心提供非常灵活的网络配置能力。
![image](https://github.com/user-attachments/assets/d6d77630-6077-4f42-b479-0793db563aaa)

###### OVS架构
![image](https://github.com/user-attachments/assets/56dd0e74-d8f0-4bdb-b633-b315c815c418)
ovs-vswitchd 为主要模块，实现交换机的守护进程daemon 
openvswitch.ko为Linux内核模块，支持数据流在内核的交换  
ovsdb-server 轻量级数据库服务器，保存配置信息，ovs-vswitchd通过这个数据库获取配置信息  
ovs-dpctl 用来配置switch内核模块  
ovs-vsctl 查询和更新ovs-vswitchd的配置  
ovs-appctl 发送命令消息，运行相关daemon  
ovs-ofctl 查询和控制OpenFlow交换机和控制器  

#### 基础资源管控
##### OpenStack的服务化架构
OpenStack的服务化架构如下图所示
![image](https://github.com/user-attachments/assets/36de3e66-5b6e-4b7e-8083-7b66a5a0f26b)

OpenStack整体由多个相互独立的服务组成，每个框图都是一个独立的服务。服务对外暴露RESTFul
API接口，服务间通过http进行交互通信，并由认证服务进行统一的身份认证和权限控制。

###### 主要的服务包括：
dashboard-Horizon：提供界面操作服务  
计算服务-nova：提供虚拟机的CRUD服务  
镜像服务-glance：提供统一的虚机镜像的存储、检索、拉取、克隆等功能  
网络服务-neutron：提供网络资源的分配管理，包括网络、子网、端口、安全组规则、路由、防火墙、负载均衡等网络能力  
块存储服务-cinder：提供块存储服务，后端可对接ceph、lvm等  
对象存储服务-swift：提供对象存储服务，兼容AWS的S3接口  
认证服务-keystone：提供服务间访问的身份认证和权限控制服务。

##### OpenStack同一服务内组件的通信交互机制
相比于相互独立的服务间通过RESTFul API互相调用的方式，服务内的组件是基于RPC进行通信和交互的。Openstack采用的是基于消息中间件-Queue（消息队列）实现的异步RPC调用。下面以计算服务nova为例介绍服务内RPC通信机制，如下图。
![image](https://github.com/user-attachments/assets/6dd258de-db5f-4537-8463-8677231959d1)

###### Nova服务内部创建虚拟机的调用流程：
nova-api组件对外暴露RESTFul API接口，并接收虚拟机创建请求；  
nova-api RPC调用nova-conductor，实现方式是将请求写入消息队列；  
nova-conductor从消息队列获取并请求RPC调用nova-scheduler，实现方式也将请求写入消息队列；  
nova-scheduler获取请求为虚拟机选取可部署的计算节点然后调用nova-compute服务，实现方式也是将请求写入消息队列；  
nova-compute从消息队列获取请求调用hpervisor及其他服务，如镜像服务、网络服务、存储服务等进行虚拟机创建；  

##### OpenStack创建虚拟机的信令流程
OpenStack创建虚拟机的信令流程如下图所示，由服务间调用和服务内调用组成，主要涉及5个服务（认证服务、计算服务、镜像服务、网络服务和块存储服务），共六类操作：1）认证与鉴权；2）计算节点调度；3）镜像拉取；4）网络资源分配；5）存储资源分配；6）基于上述资源配置并创建虚拟机
![image](https://github.com/user-attachments/assets/460ac463-0fc5-473a-a5ff-fe9ccbe96a33)
创建虚拟机的六类操作：  
服务间调用的认证与鉴权    
1、2 client登录并获取token。  
3、4、5 client调用计算服务，nova对其进行认证和鉴权    
21、24、27 nova-compute分别调用镜像服务、网络服务、块存储服务时的认证鉴权过程    

计算节点调度（计算服务内的交互）  
6、7、8、9、10、11、12、13、14、15、16、17、18、19为虚拟机选取合适的计算节点的调度过程  

镜像拉取  
20、21 请求镜像服务拉取镜像  

网络资源分配  
23、25 请求网络服务分配网络资源  

存储资源分配  
26、28 请求块存储服务分配存储资源  

配置并创建虚拟机  
29 基于上述资源配置并创建虚拟机  

#### 智能运维
##### 运维的基本概率
定义：运维是指通过一系列步骤和方法，管理与维护线上服务或产品的过程。  
对象：机房、网络、存储、物理机、虚拟机等基础设施，以及数据库、中间件平台、大数据平台等。  
职责：在产品/服务生命周期的各个阶段，保障系统的稳定运行。  
| 阶段 | 运维职责 |
|:----:|:--------|
| 设计阶段 | 稳定性评估：主要是针对系统架构设计的合理性进行评估，包括是否存在单点、可容错等，评估能够满足上线发布并稳定运行的基本要素<br>资源评估：对所需的服务器资源、网络资源以及资源的分布等进行评估，同时把握对资源申请的合理性，控制资源使用成本资源申请和准备 |
| 开发阶段 | 环境部署、依赖库及包管理、操作系统维护、数据库准备等 |
| 测试阶段 | 测试环境部署，稳定性评估 |
| 部署阶段 | 自动化部署、稳定性检验、可扩展部署等 |
| 线上运行阶段 | 保证线上服务的稳定运行：<br>实时监控：对服务运行的状态进行实时监控，随时发现服务的运行异常和资源消耗情况，输出重要的日常服务运行报表，评估服务整体运行状况，发现服务隐患<br>故障处理：对服务出现的任何异常进行及时处理，尽可能避免问题扩大化甚至中止服务<br>容量管理：包括服务规模扩张后的资源评估、扩容、机房迁移、流量调度等规划和具体实施 |
| 下线/回滚阶段 | 将服务中止，做好资源回收工作 |

##### 运维的发展历程
人工阶段  
内容：负责服务器选型、软硬件初始化、服务上下线、配置监控、查看监控等  
特点：服务器少、业务需求比较简单，少数运维工程师即可完成运维工作，不会成为业务正常运行的瓶颈；没有标准化流程，运维质量无法评估  

工具化阶段  
背景：随着行业的发展，业务系统变得愈加复杂，无法只靠人工完成运维工作  
内容：将部分运维操作及重复性工作流程编写成脚本自动执行，代替人工  
特点：简化操作流程，提升运维工作效率，降低出错概率  

平台化阶段  
背景：脚本和工具是分散、不易管理的，同时也需要人工干预，随着业务更加复杂，大量脚本的管理是低效和复杂的  
内容：将自动化脚本和工具进行整合，从系统层面构建更加易用和高效的运维管理工具，包括监控平台、报警平台和自动化平台等  
特点：提高开发和测试效率，降低运维成本，降低系统的风险概率，提高系统可用性  

智能运维阶段  
背景：尽管运维管理技术在不断进步，异常检测、故障诊断等应急操作仍需人工完成  
内容：使用机器学习和数据科学的方法，分析和处理服务、设备产生的运维数据，能够自动发现问题、解决问题  
特点：运维效率大幅提升；基础设施能够资源能够根据业务进行动态感知和自动调整，完成闭环管理，最终实现基础设施运维的“自动驾驶”  

##### 运维面对的挑战
多种异构资源组成  
多厂商异构硬件资源组成的适配和纳管  
新旧设备和软件系统的兼容  

效率要求更高  
DevOps下规划、开发、测试、交付的效率要求越来越高，出现问题需要快速解决  

海量数据处理  
随着业务发展，云资源池规模越来越大，产生大量的运维数据，这些数据的采集、处理、分析等都变的更加复杂  
多重采样类型，数据格式不统一，采集指标非标准化，难以构建运维模型  

系统更加复杂  
从一体化到分层模式，再到的为服务模式，系统架构变的更复杂  
虚拟机、中间件、容器运行时等上下游依赖变多，问题也更加难以定位和解决  

##### 智能化运维平台架构
![image](https://github.com/user-attachments/assets/a38e0406-1554-4d4f-9311-4211beee4a7e)

##### 智能化运维关键技术
云计算运维知识图谱  
提供了云计算运维知识的一种结构化表达形式，是实现智能运维的基石。  

AIOps  
提供AI运维支持，实现智能运维的更高质量、合理成本及高效支撑。  

智能化运维能力平台  
提供运维能力开放及运维服务开发，助力云基础设施平台实现智能化。  

智慧化运维部署与集成平台  
提供了基础设施智能化的各业务子系统统一编排、快速开发、持续迭代部署能力。
![image](https://github.com/user-attachments/assets/f40283d0-ecda-4f4d-bf4c-26f3be6b0ea5)


### 云原生计算基础设施核心技术 
#### 容器技术
##### 容器概述
容器是一个视图隔离、资源可限制、独立文件系统的进程集合。
![image](https://github.com/user-attachments/assets/bc5e3eb0-cf64-424b-ba5e-649e692a2304)

##### 容器生命周期
容器的生命周期可从单进程模型、数据持久化两方面进行分析：

单进程模型：
使用 docker run 的时候会指定相应的initial 进程，initial 进程启动的时候，容器也会随之启动，当 initial进程退出的时候，容器也会随之退出；因此该情况下可认为容器的生命周期和 initial 进程的生命周期是一致的；

数据持久化：
一个容器退出被删除之后，数据也会丢失，而对于有状态应用这是不被接受的，因此需要将容器所产生出来的重要数据持久化下来。容器能够直接将数据持久化到数据卷中，此时数据卷的生命周期独立于容器的生命周期，之后再把数据卷挂载到容器内，这样一来容器就能够将数据写入到相应的目录里面了，而且容器的退出并不会导致数据的丢失。

容器运行时生命周期  
单进程模型  
&emsp;&emsp;inital进程生命周期=容器生命周期  
&emsp;&emsp;运行期间可运行exec执行运维操作  
数据持久化  
&emsp;&emsp;独立于容器的生命周期  
&emsp;&emsp;数据卷管理：  
&emsp;&emsp;&emsp;&emsp;1. 通过bind方式进行管理  
&emsp;&emsp;&emsp;&emsp;2. 将目录管理交给容器运行引擎  

##### 容器与虚拟机对比
容器和虚拟机相同点包括：
1. 都需要对物理硬件资源进行共享使用；
2. 生命周期相似；
3. 均可安装各种应用；
4. 创建后都会存储在宿主机上。
不同点如下:
![image](https://github.com/user-attachments/assets/8429421f-a7b8-4f1d-9897-fbc395c1d9ca)

#### Kubernetes原理介绍 
Kubernetes是一个全新的基于容器技术的分布式架构解决方案，且是一个一站式的完备的分布式系统开发和支撑平台。随着云计算技术的发展，Kubernetes如今已成为容器编排的事实标准。在集群管理方面，Kubernetes将集群中的及其划分为一个Master节点和多个Node节点：

Master节点：  
运行集群管理相关的一组进程，包括：kube-apiserver、kube-controller-Manager、kube-scheduler，负责实现整个集群的资源管理、Pod调度、弹性伸缩、安全控制、系统监控和纠错等管理功能；

Node节点：  
集群的工作节点，运行真正的应用程序；Node上运行着Kubernetes的kubelet、kube-proxy服务进程，这些进程负责Pod的创建、启动、监控、重启和销毁，以及实现软件模式的负载均衡器。
![image](https://github.com/user-attachments/assets/8a159247-881d-4802-81e3-c9369e7a18aa)

#### Kubernetes核心概念
Kubernetes中有五个核心概念，分别是：Pod、Volume、Deployment、Service及Namespace  

Pod：  
最小的调度、资源单位  
由一个或多个容器组成  
定义容器运行的方式（通过Command、环境变量等）  
提供给容器共享的运行环境（网络、进程空间）  

Volume：  
声明在Pod中的容器可访问的文件目录  
可被挂载在Pod中一个或多个容器的指定路径下  
支持多种后端存储的抽象，如本地存储、分布式存储、云存储等  

Deplyment：  
定义一组Pod的副本数目、版本等  
通过Controller维持Pod的数目，可自动恢复失败的Pod  
通过控制器以指定的策略控制版本；如滚动升级、重新生成、回滚等  
  
Service：  
提供访问一个或多个Pod实例的稳定访问地址  
支持多种访问方式实现    
ClusterIP  
NodePort  
LoadBalancer  

Namespace：  
一个集群内部的逻辑隔离机制（鉴权、资源管理等）；  
每个资源都属于一个Namespace  
同一个Namespace中的资源命名唯一  
不同Namespace中的资源可重名  

#### Kubernetes关键组件
##### API Server
Kubernetes API Server的核心功能是提供Kubernetes各类资源对象（如Pod、RC、Service等）的增删改查、Watch等HTTP Rest接口，它是集群内各个功能模块之间数据交互和通信的中心枢纽，是整个Kubernetes系统的数据总线及数据中心；除此之外，它还具有如下功能特性：

是集群管理的API 入口  
是资源配额控制的入口  
提供了完备的集群安全机制  

架构解析  
API Server架构从上至下可划分为如下四层：  

API层  
主要以REST方式提供各种API接口，包括：K8S资源对象的CRUD和Watch等主要API；健康检	查、UI、日志、性能指标等运维监控相关的API；  

访问控制层  
负责对用户身份进行鉴权，根据资源访问许可逻辑（Admission Control）核准是否允许其访问；  

注册表层  
K8s所有的资源对象均保存在注册表（Registry）中  

etcd数据库  
用于持久化存储Kubernetes资源对象的KV数据库  
![image](https://github.com/user-attachments/assets/4d71d3c3-44f4-47c9-be66-ae98e8a5d140)

##### Controller Manager
Controller Manager是Kubernetes中各种操作系统的管理者，是集群内部的管理控制中心，也是Kubernetes自动化功能的核心。
通过API Server提供的List-Watch接口实时监控集群中特定资源的状态变化，当发生各种故障导致某资源对象的状态发生变化时，Controller会尝试将其状态调整为期望的状态，确保集群始终处于预期的工作状态。
如下图所示，Controller Manager内部包含8种Controller，每种Controller负责一种特定资源的控制流程，而Controller Manager是这些Controller的核心管理者。
![image](https://github.com/user-attachments/assets/0d551343-a7b9-4760-91fd-29916be21acb)

##### Scheduler
Kubernetes Scheduler负责Pod调度，其作用是将待调度的Pod按照特定的调度算法和调度策略绑定（Binding）到某个合适的Node上，并将绑定信息写入到etcd中。它在Kubernetes系统中起到“承上启下”的作用：  

承上：负责接收Controller Manager创建的新Pod，并为其分配到目标Node上；  

启下：在安置工作完成后，目标Node上的Kubelet服务进程接管后继工作，负责Pod之后的生命周期。  
![image](https://github.com/user-attachments/assets/f9ce44d6-727f-4e66-b5cd-6c6ad2e4b202)

##### kubelet&kube-proxy
###### kubelet
Kubernetes集群中，每个Node上都会启动一个kubelet服务进程；该进程负责处理Master下发到本节点的任务，管理Pod及Pod中的容器  
每个kubelet进程都会在API Server上注册节点自身的信息，定期向Master汇报节点资源的使用情况，并通过cAdvisor监控容器和节点资源  

kubelet主要功能如下：  
&emsp;&emsp;节点管理  
&emsp;&emsp;Pod管理  
&emsp;&emsp;容器健康检查  
&emsp;&emsp;&emsp;&emsp;1. LivenessProbe探针  
&emsp;&emsp;&emsp;&emsp;2. ReadinessProbe探针  
&emsp;&emsp;cAdvisor资源监控
  
kube-proxy
Kubernetes集群中，每个Node上都会启动一个kubeproxy服务进程；可将该进程视为Service的透明代理兼负载均衡器，其核心功能是将某个Service的访问请求转发到后端的多个Pod实例上
kube-proxy 针 对 Service 和 Pod 创 建 的 一 些主要iptables规则如下：
1. KUBE-CLUSTER-IP：在指定情况下对Service Cluster IP地址进行伪装，以解决数据包欺骗问题；
2. KUBE-EXTERNAL-IP：将数据包伪装成Service的外部IP地址；
3. KUBE-LOAD-BALANCER,KUBE-LOAD-BALANCERLLOCAL：伪装Load Balancer类型的Service流量
4. KUBE-NODE-PORT-TCP等：伪装NodePort类型的Service流量

#### Kubernetes存储概述
Kubernetes对于有状态的应用或者对数据需要持久化的应用，提供了可靠的存储机制来保存应用产生的重要数据，可以确保容器应用在重建之后仍然可以使用原有的数据。在Kubernetes中屏蔽了底层存储的实现细节，因此没有传统的块存储、文件存储等存储概念，它从管理员的管理视角、用户的使用视角引入了对应的PV（Persistent Volume）和PVC（Persistent Volume Claim）两个资源对象实现对存储的管理。

PV：是对底层网络共享存储的抽象，是一种可供容器应用消费的资源。PV与实际的存储系统直接对应，它后端对应的既可以是类似云硬盘的块设备，也可以是一个共享文件系统。因为与实际的存储系统有关，因此PV一般需要由管理员进行创建、销毁等管理操作。

PVC：是用户对存储资源的一个使用申明，用户只需要创建PVC，系统会根据用户申明的空间大小、读写模式等自动绑定到一个合适的PV上，这样用户就可以实际使用PV对应的后端存储。

StorageClass：从以上可以看出，管理员负责创建PV，用户通过PVC消费PV，这个过程相对割裂，没有足够的自动化，无法满足容器应用的敏捷性要求。因此，Kubernetes引入了StorageClass的概念，管理员可以将存储资源定义为某种类别（Class），用户指定StorageClass即可实现对存储资源的申请，这样就实现了存储系统的动态供应，实现了存储卷的按需创建，真正做到了共享存储的自动化管理。

CSI：Kubernetes从1.9版本开始引入容器存储接口Container Storage Interface（CSI）机制，目标是在Kubernetes和外部存储系统之间建立一套标准的存储管理接口，通过该接口提供存储服务

##### PV
PV作为存储资源，是与后端实际的存储系统直接关联的，它可以是块存储系统提供的一个块设备，比如分布式存储系统Ceph的RBD、传统存储阵列的Lun；也可以是共享文件存储系统，比如NFS的一个共享目录。因为与实际存储系统有关，所以PV主要包括了下面几项关键信息。  
&emsp;&emsp;存储能力：当前主要是指存储空间（比如5Gi），未来可能会支持IOPS、IO带宽等其他存储指标；  
&emsp;&emsp;存储卷模式：主要是指后端存储类型是文件系统（Filesystem）还是块设备（Block）  
&emsp;&emsp;访问模式：PV的访问模式代表了应用对存储的访问权限，主要包括如下三种：  
&emsp;&emsp;&emsp;&emsp;ReadWriteOnce：读写权限，只能被单个Node挂载  
&emsp;&emsp;&emsp;&emsp;ReadOnlyMany：只读权限，允许被多个Node挂载  
&emsp;&emsp;&emsp;&emsp;ReadWriteMany：读写权限，允许被多个Node挂载  
&emsp;&emsp;回收策略：支持保留、回收空间、删除三种策略  
&emsp;&emsp;挂载参考：与具体后端存储类型有关，不同后端存储挂载参数存在差异  
&emsp;&emsp;节点亲和性：通过节点亲和性可以确保PV只能被某些Node访问，使用这些PV的POD也就只能被调度到这些Node上  

*Tips：PV的生命周期独立于POD的生命周期，Kubernetes通过引入PV实际上是实现了存储于计算的分离，解耦了POD与Volume生命周期关联。*
![image](https://github.com/user-attachments/assets/11f082c9-a409-4d8e-853b-e3ebd83459c5)

##### PVC
PVC是用户对存储资源申请的说明，主要包括存储空间、访问模式等信息，这些说明与PV的关键信息是对应的。Kubernetes系统会根据用户PVC的申明，自动绑定到符合条件的PV上。  
在Kubernetes中引入PVC主要原因在于职责分离：PVC是用户申明的，用户只需要关系自己所需存储的空间、读写模式等信息，而不需要关心存储后端；与存储后端相关的信息在PV中，这部分是由管理员统一运维和管控的。
![image](https://github.com/user-attachments/assets/4a2f95fa-5947-4cc6-a1a3-6dc1a5a8ef5a)

##### StorageClass
StorageClass实现了Volume的动态创建，可以认为StorageClass是前面介绍的创建PV的模板，它包含了创建某种具体类型PV所需的参数信息，用户创建PVC时指定所用的SC，系统会自动创建对应的PV，并将PV绑定到PVC。使用SC，可以最大程度减轻管理云手工管理PV的工作负担。
![image](https://github.com/user-attachments/assets/3fbc747b-d2b7-4792-91c1-3af67688408b)

##### CSI机制
CSI是Kubernetes推出的与容器对接的存储接口标准，存储提供方只需要基于标准接口进行存储插件的实现，就能使用Kubernetes的原生存储机制为容器提供存储服务。在CSI成为Kubernetes的存储接口标准以后，存储供应方的代码有存储插件开发方进行维护，和Kubernetes的代码彻底解耦，部署也与Kubernetes核心组件分离。基于CSI的存储插件机制也称为“out of tree”的服务提供方式，是未来Kubernetes第三方存储插件的标准方案。
 
CSI主要包括两种组件：  
&emsp;&emsp;CSI Controller：它的功能是提供存储服务视角对存储资源和存储卷进行管理和操作，一般将其部署为单副本POD，可以使用StatefulSet或者Deployment控制器进行部署。CSI Controller中包含了CSI Driver，通过这些Driver，CSI Controller与外部存储系统进行交互，实现实际存储卷的创建、删除等操作。  
&emsp;&emsp;CSI Node：它主要功能是对Node节点上的Volume进行管理和操作，由于需要在所有Node节点上部署，因此建议将其部署为DaemonSet。CSI Node中也包含了CSI Driver，这里的CSI Driver主要功能是实现与Node相关的卷操作功能，比如将创建好的Volume挂载在Node上。

#### Kubernetes网络概述
Kubernetes网络设计遵循并满足：  
一个基础原则：  
&emsp;&emsp;每个Pod都拥有一个独立的IP地址，并假定所有Pod都在一个可以直接连通的、扁平的网络空间中。  

三个基本条件：  
&emsp;&emsp;所有Pod可以与其他Pod直接通信，无需显示使用NAT  
&emsp;&emsp;所有Node可以与所有Pod直接通信，无需显示使用NAT  
&emsp;&emsp;Pod可见的IP地址和对外展示给用户的IP是同一个  

基于以上原则及条件，Kubernetes网络方案需要考虑如下：  
四大目标：  
&emsp;&emsp;容器与容器之间的通信  
&emsp;&emsp;Pod与Pod之间的通信  
&emsp;&emsp;Pod与Service之间的通信  
&emsp;&emsp;集群外部与内部组件之间的通信  

#### Kubernetes 网络实现
##### 容器到容器
同一Pod内的容器共享同一个网络命名空间，共享同一个Linux协议栈。因此容器到容器之间的网络通信，可视为它们在同一台机器上，甚至可用localhost地址访问彼此的端口，不需要针对网络进行特别的修改。  
Kubernetes的Pod网络模型如下图所示：
![image](https://github.com/user-attachments/assets/7931b8e3-225a-4424-a24e-0e55e10e0017)

##### Pod到Pod
每一个Pod都有一个真实的全局IP地址，同一个Node内的不同Pod之间可以直接采用对方Pod的IP地址通信，且不需要采用其他发现机制，如DNS、Consul或etcd。根据Pod所处的Node，Pod间的通信可划分为如下两类：  
同一Node内Pod之间的通信
![image](https://github.com/user-attachments/assets/1f290909-8c9f-44a0-8d98-0ee0dc6bea99)
&emsp;&emsp;Pod1和Pod2均通过Veth连接到同一个docker0网桥上，他们的IP地址IP1、IP2与网桥本身的IP3属于同一网段  
&emsp;&emsp;Pod1和Pod2的Linux协议栈上默认路由均为docker0的地址，因此所有非本地地址的网络数据，都会被默认发送到docker0网桥上，由docker0网桥直接中转

不同Node上Pod之间的通信  
![image](https://github.com/user-attachments/assets/2e3cf801-7101-4506-9e3e-3df56f2bfce3)
Pod1在访问Pod2时，首先要将数据从源Node的eth0发送出去，找到并到达Node2的eth0,即先完成IP3到IP4的传递，在完成IP4到IP2的传递














