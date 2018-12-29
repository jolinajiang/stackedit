# ISTIO
## 架构
Istio服务网格逻辑上分为**数据平面**和**控制平面**

- **数据平面**由一组以sidecar方式不是的智能代理[Envoy](https://www.envoyproxy.io/)组成。这些代理可以调节和控制微服务及[Mixer](https://preliminary.istio.io/zh/docs/concepts/policies-and-telemetry/)之间所有的网络通信。
- **控制平面**负责管理和配置代理路由流量。此外控制平面配置Mixer以实施策略和收集遥测数据。

架构图如下：
![Istio架构图](https://preliminary.istio.io/docs/concepts/what-is-istio/arch.svg )
### Envoy
Istio使用[Envoy](https://www.envoyproxy.io/)代理的扩展版本，Envoy是以C++开发的高性能代理，用于调节服务网格中所有服务的入站和出战流量。Envoy的许多内置功能被istio发扬光大，例如：

- 动态服务发现
- 负载均衡
- TLS终止
- HTTP/2 & gRPC代理
- 熔断器
- 健康检查、基于百分比流量拆分的灰度发布
- 故障注入
- 丰富的度量指标

Envoy被部署为**sidecar**，和对应服务在同一个Kubernetes pod中。
### Mixer
[Mixer](https://preliminary.istio.io/zh/docs/concepts/policies-and-telemetry/)是一个独立于平台的组件，负责在服务网格中执行访问控制和使用策略，并从Envoy代理和其他服务收集遥测数据。代理提取请求级[属性](https://preliminary.istio.io/zh/docs/concepts/policies-and-telemetry/#%E5%B1%9E%E6%80%A7)，发送到Mixer进行评估。
### Pilot
[Pilot](https://preliminary.istio.io/zh/docs/concepts/traffic-management/#pilot-%E5%92%8C-envoy)为Envoy sidecar提供服务发现功能，为智能路由（例如A/B测试，金丝雀部署等）和弹性（超时、重试‘熔断器等）提供流量管理功能。它将控制流量行为的高级路由规则特定于Envoy的配置，并在运行时将它们传播到sidecar。
### Citadel
[Citadel](https://preliminary.istio.io/zh/docs/concepts/security/)通过内置身份和凭证管理可以提供强大的服务间和最终身份验证。可用于升级服务网格中未加密的流量，并为运维人员提供基于服务标识而不是网络控制的强制执行策略的能力。从0.5版本开始，Istio支持[基于角色的访问控制](https://preliminary.istio.io/zh/docs/concepts/security/#%E8%AE%A4%E8%AF%81)，以控制可以访问您的服务。

### 设计目标
Istio的架构设计中有几个关键目标，这些目标对于使系统能够应对大规模流量和高性能地服务处理至关重要。

- **最大化透明度**：若想Istio被采纳，应该让运维和开发人员只需付出很少的代价就可以从中获益。为此，Istio将自身自动注入到服务间所有的网络路径中。Istio使用sidecar代理来捕获流量，并且在尽可能的地方自动编程网络层，以路由流量来通过这些代理，而无需对已部署的应用程序代码进行任何改动。
- **增量**
- **可移植性**
- **策略一致性**

## 流量管理
使用Istio的流量管理模型，本质上是将流量与基础设施扩容解耦，让运维人员可以通过Pilot指定流量遵循什么规则，而不是指定哪些pod/VM应该接收流量——Pilot和智能Envoy代理会帮我们搞定。
![Istio æµé‡ç®¡ç†](https://preliminary.istio.io/docs/concepts/traffic-management/TrafficManagementOverview.svg)
将流量从基础设施中解耦，这样就可以让Istio提供各种独立于应用程序代码之外的流量管理功能。除了A/B测试的动态[请求路由](https://preliminary.istio.io/zh/docs/concepts/traffic-management/#%E8%AF%B7%E6%B1%82%E8%B7%AF%E7%94%B1)，逐步推出和金丝雀发布之外，它还使用超时、重试和熔断器来处理[故障恢复](https://preliminary.istio.io/zh/docs/concepts/traffic-management/#%E6%95%85%E9%9A%9C%E5%A4%84%E7%90%86)，最后还可以通过[故障注入](https://preliminary.istio.io/zh/docs/concepts/traffic-management/#%E6%95%85%E9%9A%9C%E6%B3%A8%E5%85%A5)









<!--stackedit_data:
eyJoaXN0b3J5IjpbNDM3NjQ4NDk3LDQ0ODM4NzQ3NywtOTEzND
g5NTkxLC00NTE2MDk5MDMsMTM3OTkzMjE0NiwxMjE4OTk0NTMs
Njk3MTIyMzcyLDc3OTM5NzU1LC0yMTA4MTY4OTY4LDYzMDk4MT
A5MCwxODczMTIzNTYwLC0xNTg5MzY5OTk5LDczMDk5ODExNl19

-->