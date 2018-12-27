# ISTIO
## 架构
Istio服务网格逻辑上分为**数据平面**和**控制平面**

- **数据平面**由一组以sidecar方式不是的智能代理[Envoy](https://www.envoyproxy.io/)组成。这些代理可以调节和控制微服务及[Mixer](https://preliminary.istio.io/zh/docs/concepts/policies-and-telemetry/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTExNDg5NzExNSwxODczMTIzNTYwLC0xNT
g5MzY5OTk5LDczMDk5ODExNl19
-->