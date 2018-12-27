# SOFA Mesh的技术选型

## 性能要求
 - 以蚂蚁金服的体量，性能不够好则难于接受；
 - 架构与性能之间的权衡和取舍需要谨慎考虑；
## 稳定性要求
 - 以蚂蚁金服的标准，稳定性的要求自然是很高；
 - **高可用方面**的要求会非常高
## 部署的要求
 - 需要用于多种场合：主站，金融云，外部客户
 - 需要满足多种部署环境：虚拟机/容器，公有云/私有云,k8s
 - 需要满足多种体系：Service Mesh,Sofa和社区主流开发框架
## Sofa Mesh在技术选型时考虑
 - Envoy  数据平面：Envoy最符合要求，XDS API的设计更是令人称道，C++带来的技术栈选择问题
 - Istio	控制平面：Istio是目前做的最好的，认可Istio的设计理念和产品方向，性能和稳定性是目前最大问题，对非k8s环境的支持不够理想，没有提供和侵入式框架互通的解决方案
![架构对比](https://pic2.zhimg.com/80/v2-a6cb5bc29ca3c5d3b3c5ae4f5bfe2f51_hd.jpg)
左边是Istio现有的架构,Envoy/Pilot/Mixer/Auth
右边是我们**SOFA Mesh**的架构：
1、最重要的一点：用Golang开发的Sidecar替换Envoy，用Golang重写整个数据平面；
2、合并一部分Mixer内容到Sidecar
3、Pilot和Auth会做扩展和增强
## 技术选型的实现
![Golang版Sidecar](https://pic1.zhimg.com/80/v2-04eec770ee19e1fa3ac2758da1b3cc7c_hd.jpg)
### Golang版本的Sidecar
支持标准的HTTP/1.1和HTTP/2，也就是常见的REST和gRPC协议。然后会增加一些特殊的协议扩展，包括Sofa协议，Dubbo协议，HSF协议，mixer service部分没有改动。
![preview](https://pic3.zhimg.com/v2-94dd7678c9dbb52b8897fb24d0c00ef6_r.jpg)
最大变化在Mixer，Sidecar替换Envoy而已，架构上没有变化。
Mixer三大功能：
 - check，也叫precondition,前置条件检查，比如说黑白名单，权限；
 - quota，比如说访问次数之类；
 - report，比如说日志，度量等。

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MjM5MTA4ODYsNTAxMTkyNTk2LC03OD
QwMDYzMzRdfQ==
-->