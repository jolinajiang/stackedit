# ISTIO
## 架构
Istio服务网格逻辑上分为**数据平面**和**控制平面**

- **数据平面**由一组以sidecar方式不是的智能代理[Envoy](https://www.envoyproxy.io/)组成。这些代理可以调节和控制微服务及[Mixer](https://preliminary.istio.io/zh/docs/concepts/policies-and-telemetry/)之间所有的网络通信。
- **控制平面**负责管理和配置代理路由流量。此外控制平面配置Mixer以实施策略和收集遥测数据。

架构图如下：
![Istio架构图](https://preliminary.istio.io/docs/concepts/what-is-istio/arch.svg )


















<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDgxNjg5NjgsNjMwOTgxMDkwLDE4Nz
MxMjM1NjAsLTE1ODkzNjk5OTksNzMwOTk4MTE2XX0=
-->