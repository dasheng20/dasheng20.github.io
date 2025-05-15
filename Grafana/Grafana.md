# Grafana

## 介绍

> 两个核心功能是**仪表板**和**告警**。Grafana支持常用的关系型数据库及Prometheus（时序数据库）。连接数据源后构建SQL或直接写SQL可以构建出仪表板和要告警数据。仪表板支持多种常用图表，包含柱状图、折线图、饼图等。告警支持多种发送方式，包含邮箱、钉钉、webhook等。

### 概念解释



## 安装

### docker 安装

**docker-compose.yml**

```yaml
services:
  grafana:
    image: grafana/grafana:11.0.0
    container_name: grafana
    restart: always
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin
      - GF_PLUGINS_ALLOW_LOADING_UNSIGNED_PLUGINS=albertowd-oraclegrafana-datasource
    volumes:
      - grafana-data:/var/lib/grafana
      - /usr/local/software/grafana/plugins:/var/lib/grafana/plugins  
      - /usr/local/software/grafana/grafana.ini:/etc/grafana/grafana.ini
      - /usr/local/software/grafana/emails:/usr/share/grafana/public/emails
      - /usr/local/software/grafana/alert_rules:/etc/grafana/provisioning/alerting
      - /usr/local/software/grafana/datasources:/etc/grafana/provisioning/datasources
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: always
    ports:
      - "9091:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml   
        #    command:
        # - "--config.file=/etc/prometheus/prometheus.yml"
volumes:
  grafana-data:
    driver: local
```



## 功能介绍

### 	看板

### 	告警

#### 发送模板自定义

#### 告警规则的导入导出



## 其他

1. **非企业版不支持Oracle数据库，需手动安装第三方数据库插件**

