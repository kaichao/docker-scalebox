# 1. Scalebox介绍

## 1.1 技术起源

容器化作为新一代云计算技术，广泛应用于互联网行业的大规模云服务部署。容器云有效解决了超大规模互联网服务的可扩展性，大幅提升服务可靠性；容器化还可简化软件部署，提高软件研发管理的效率。

在高性能计算/大数据分析等方向上，作为应用封装技术的容器化也得到广泛应用。
- 容器化可解耦算法专业性及大数据处理，使得应用领域、大数据平台各自聚焦，实现职责分离、协作分工。
- 复杂工业软件研发中，流程复杂、算法专业性强，其软件复用难度大。容器化实现软件部署的封装，简化集成测试，降低软件研发成本，缩短研发周期，提升软件质量。

当前容器化应用形式主要体现在对各类网络服务的封装。与成熟的服务容器化相比，容器化计算正成为一个新的技术方向。

当前主要的容器化计算形式：
- 轻量级虚拟化：以容器封装算法的复杂依赖及运行时，并通过ssh或容器执行等方式进入容器，利用命令行来运行算法，以简化算法实验、代码调试。
- 算法容器化封装：以容器镜像定义封装算法，实现以统一的容器资源层接口（南向接口）对接底层计算平台。通过调度系统、工作流引擎或外部命令来实例化容器并运行算法。
- 可编程容器化计算：以容器化封装为基础，定义统一的算法容器应用接口（北向接口）规范，以消息驱动标准化算法容器的运行。

基于可编程容器化计算的并行程序，在架构上将复杂计算逻辑分层，分解为算法逻辑和并行逻辑。算法逻辑对应算法自身，封装于标准化、消息驱动式的容器。并行逻辑则处理算法并行化相关的业务逻辑，包括资源调度、数据分布、任务分配、通信原语、流控处理等。并行逻辑中，任务分配设计为数据驱动式的非冯诺依曼架构，计算由数据可用性驱动，而非程序指令顺序/并行驱动，实现最大化的并行。通过标准容器的组合及级联，支持复杂计算逻辑。以这种方式构建的分布式并行计算程序，具有传统容器化封装简化软件编程，兼备在大规模、分布式计算设施上充分并行的优势。

## 1.2 Scalebox是什么？

Scalebox是一种可编程容器化计算框架，以容器化封装算法并提供可编程特性，支持在分布式、异构环境上的跨集群流式计算。计算任务以非冯诺依曼架构的数据流驱动，实现超大规模并行。框架支持本地数据加载、任务级容错，其应用场景包括高通量复杂流水线、分布式算力、嵌入式多平台分布式仿真等应用场景。

Scalebox应用程序采用分层组织。模块层将算法模块封装为标准容器，并提供消息驱动式容器层接口；应用层通过消息路由模块实现消息分发，完成应用逻辑。分层架构简化大型、复杂系统的软件研发。应用程序的计算编排，以声明式的方式支持大规模复杂应用的在HPC、大规模集群上的运行调度。
以非侵入式封装算法，形成标准模块；在Scalebox编程框架层，以消息驱动形式调用标准模块，以串行方式实现并行程序，；

- 大数据处理平台：在支持高通量数据加载上
- 并行计算框架（北向接口）：面向应用需求，支持并行程序开发
- 容器化计算的编排调度（南向）：简化与底层计算资源的耦合。

Scalebox是一种云原生的流式并行计算引擎，Scalebox应用支持广域网跨集群部署、任务级容错、多级存储的数据加载等特性，并支持容器间流水线并行、容器级数据级并行、容器内代码并行等多级并行化。其技术特点特别适用于数据分布、算力分布、复杂算法封装、极高强度I/O读写等应用场景。简化超大规模并行数据处理的实现。

Scalebox应用程序的构建，按统一技术规范，做用户算法的容器化封装，形成消息驱动式的标准模块。通过串行的脚本编程，将容器化算法构建为在分布式、异构、多集群环境下、以流式方式运行的并行计算程序。

基于容器化计算技术，实现计算任务的容器编排、任务调度。

主要特性包括：
- 云原生设计
- 非侵入式：通过
- 跨集群部署：
- 本地计算
- 任务透视及优化支持

## 1.3 Scalebox能做什么？

- Scalebox非常适用于超大规模高通量数据处理，尤其适用于中间数据规模超大的场景。

### 1.3.1 大规模数据的复杂处理
- 复杂流水线应用
  - 天文计算：大型天文望远镜收集太空的观测数据，其数据量巨大，其数据处理通常需要巨量计算资源和复杂的数据分析技术。
  - 基因组学和生物信息学：包括基因组测序、基因组组装、基因组比对、蛋白质结构预测等应用，并利用计算来分析和解释这些数据。
  - 高能物理：包括粒子对撞机实验、核物理实验等。这些实验产生了大量高能物理数据，需大量计算资源和复杂分析算法来研究和解释这些数据。

	支持容错数据处理：针对各类异常（低成本硬件异常、系统软件运行时异常、用户代码出错、数据异常等）的容错处理；实现可复算、可管理的科学数据分析；

### 1.3.2 跨集群算力应用

- 大规模数据传输：利用横向扩展支持数据传输，通过数据压缩提升网络带宽利用，通过数据校验提升网络传输的可靠性，利用流水线并行提升运行效率。

### 1.3.3 基于容器化的跨平台嵌入式仿真

- 按统一技术规范，对不同平台嵌入式应用的容器化封装，提供统一的北向接口
- 利用标准模块的可编程接口，Scalebox平台支持不同类型的应用功能，实现对标准模块的管理、控制
- 主要功能
  - 软件模块标准化封装
  - 模块级自动化测试
  - 多平台、多模块集成测试
  - 多平台复杂应用的全系统仿真


## 参考文献

<a id="1">[1]</a> Bentaleb, O., Belloum, A.S.Z., Sebaa, A. et al. Containerization technologies: taxonomies, applications and challenges. J Supercomput 78, 1144–1181 (2022). 
https://doi.org/10.1007/s11227-021-03914-1

<a id="2">[2]</a> D. Bernstein, "Containers and Cloud: From LXC to Docker to Kubernetes," IEEE Cloud Computing, vol. 1, no. 3, pp. 81-84, Sept. 2014.
https://doi.org/10.1109/MCC.2014.51

<a id="3">[3]</a> M. J. Scheepers, "Virtualization and containerization of application infrastructure: A comparison", Proc. 21st Twente Student Conf. IT, 2014, pp. 1–7.

<a id="4">[4]</a> J. Watada, A. Roy, R. Kadikar, H. Pham and B. Xu, "Emerging Trends, Techniques and Open Issues of Containerization: A Review," in IEEE Access, vol. 7, pp. 152443-152472, 2019. 
doi: 10.1109/ACCESS.2019.2945930.
https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8861307

<a id="5">[5]</a> Alser, M., Lawlor, B., Abdill, R.J. et al. Packaging and containerization of computational methods. Nat Protoc 19, 2529–2539 (2024). 
https://doi.org/10.1038/s41596-024-00986-0

