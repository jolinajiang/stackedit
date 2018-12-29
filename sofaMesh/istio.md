# ISTIO
## 架构
Istio服务网格逻辑上分为**数据平面**和**控制平面**

- **数据平面**由一组以sidecar方式不是的智能代理[Envoy](https://www.envoyproxy.io/)组成。这些代理可以调节和控制微服务及[Mixer](https://preliminary.istio.io/zh/docs/concepts/policies-and-telemetry/)之间所有的网络通信。
- **控制平面**负责管理和配置代理路由流量。此外控制平面配置Mixer以实施策略和收集遥测数据。

架构图如下：
![Istio架构图](https://preliminary.istio.io/docs/concepts/what-is-istio/arch.svg )
## Envoy
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
## Mixer
[Mixer](https://preliminary.istio.io/zh/docs/concepts/policies-and-telemetry/)是一个独立于平台的组件，负责在服务网格中执行访问控制和使用策略，并从Envoy代理和其他服务收集遥测数据。代理提取请求级[属性](https://preliminary.istio.io/zh/docs/concepts/policies-and-telemetry/#%E5%B1%9E%E6%80%A7)，发送到Mixer进行评估。
## Pilot
[Pilot](https://preliminary.istio.io/zh/docs/concepts/traffic-management/#pilot-%E5%92%8C-envoy)为Envoy sidecar提供服务发现功能，为智能路由（例如A/B测试，金丝雀部署等）













<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIxODk5NDUzLDY5NzEyMjM3Miw3NzkzOT
c1NSwtMjEwODE2ODk2OCw2MzA5ODEwOTAsMTg3MzEyMzU2MCwt
MTU4OTM2OTk5OSw3MzA5OTgxMTZdfQ==
-->