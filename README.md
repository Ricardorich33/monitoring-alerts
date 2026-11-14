# monitoring-alerts

Prometheus 告警规则示例，覆盖主机、容器和接入层常见异常，适合配合 `docker-compose-stacks/monitoring` 使用。

## 规则说明

`prometheus/rules.yml` 包含几类规则：

- 主机：CPU、内存、磁盘、节点失联。
- 容器：容器退出、频繁重启（需要 cAdvisor 提供容器指标）。
- 接入层：HTTP 探测失败、响应时间过高（需要 blackbox-exporter）。

## 使用

1. 把 `rules.yml` 挂载到 Prometheus 的规则目录。
2. 容器指标需要 cAdvisor，HTTP 探测需要 blackbox-exporter，按需补充 scrape 配置。
3. `alertmanager.yml` 是告警路由示例，默认接入钉钉机器人，替换 token 即可使用。
4. 把 `grafana/node-exporter-overview.json` 导入 Grafana，导入时选择你的 Prometheus 数据源即可。

> 阈值需要根据业务实际调整，不要把示例值直接用于生产。
