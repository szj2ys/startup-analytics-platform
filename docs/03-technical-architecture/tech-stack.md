# 🏗️ 技术架构与选型

> 最后更新：2026-03-11

---

## 一、技术架构总览

```
┌─────────────────────────────────────────────────────────────────┐
│                        用户层 (User Layer)                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  Web Dashboard │  Mobile App  │  Embedded Analytics        │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API 网关层 (API Gateway)                    │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  REST API   │  │  GraphQL    │  │  WebSocket  │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│  ┌─────────────────────────────────────────────────────┐       │
│  │  认证授权 (Auth) │  限流 (Rate Limit) │  路由       │       │
│  └─────────────────────────────────────────────────────┘       │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      服务层 (Service Layer)                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │ 用户服务    │  │ 分析服务    │  │ 报表服务    │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │ 事件服务    │  │ 查询服务    │  │ 通知服务    │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      数据层 (Data Layer)                         │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │ 消息队列    │  │ 流处理      │  │ 批处理      │             │
│  │ (Kafka)     │  │ (Flink)     │  │ (Spark)     │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│  ┌─────────────────────────────────────────────────────┐       │
│  │              数据存储 (Storage)                      │       │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐  │       │
│  │  │ClickHouse│ │PostgreSQL│ │  Redis  │ │  MinIO  │  │       │
│  │  │ (分析)   │ │ (元数据) │ │ (缓存)  │ │ (文件)  │  │       │
│  │  └─────────┘ └─────────┘ └─────────┘ └─────────┘  │       │
│  └─────────────────────────────────────────────────────┘       │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    数据采集层 (Data Collection)                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │ JavaScript  │  │  iOS SDK    │  │ Android SDK │             │
│  │    SDK      │  │             │  │             │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │ Python SDK  │  │  Java SDK   │  │   HTTP API  │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────────────────────────────────────────────────┘
```

---

## 二、核心技术选型

### 2.1 后端技术栈

| 层级 | 技术选型 | 备选方案 | 选择理由 |
|------|----------|----------|----------|
| **编程语言** | Python 3.11+ | Go, Node.js | 生态丰富，数据分析库多，开发效率高 |
| **Web框架** | FastAPI | Django, Flask | 异步支持好，性能高，API文档自动生成 |
| **数据库** | PostgreSQL 15+ | MySQL | JSON支持好，扩展性强，生态成熟 |
| **分析引擎** | ClickHouse 24+ | Apache Druid, StarRocks | 高性能OLAP，实时分析，开源免费 |
| **缓存** | Redis 7+ | Memcached | 数据结构丰富，持久化，发布订阅 |
| **消息队列** | Apache Kafka | RabbitMQ, NATS | 高吞吐，持久化，生态成熟 |
| **对象存储** | MinIO | AWS S3, 阿里云OSS | 兼容S3，可私有化部署 |

### 2.2 前端技术栈

| 层级 | 技术选型 | 备选方案 | 选择理由 |
|------|----------|----------|----------|
| **框架** | React 18+ | Vue 3, Angular | 生态最丰富，可视化库多 |
| **语言** | TypeScript 5+ | JavaScript | 类型安全，IDE支持好 |
| **构建** | Vite 5+ | Webpack, Rollup | 启动快，配置简单 |
| **状态管理** | Zustand | Redux, MobX | 轻量，简单，现代化 |
| **样式** | Tailwind CSS | Styled Components | 开发快，一致性高 |
| **可视化** | Apache ECharts | D3.js, AntV | 功能全面，中文文档好 |
| **组件库** | Ant Design 5+ | Material-UI | 企业级组件，生态成熟 |

### 2.3 基础设施

| 层级 | 技术选型 | 备选方案 | 选择理由 |
|------|----------|----------|----------|
| **容器** | Docker | containerd | 生态标准，易用性好 |
| **编排** | Kubernetes | Docker Swarm | 行业标准，扩展性强 |
| **网关** | Kong | Nginx, Traefik | 功能丰富，插件生态好 |
| **监控** | Prometheus + Grafana | DataDog | 开源，云原生标准 |
| **日志** | ELK Stack (简化版) | Loki | 功能全面，社区活跃 |
| **CI/CD** | GitHub Actions | GitLab CI | 与GitHub集成好 |

---

## 三、数据架构详细设计

### 3.1 数据流架构

```
┌─────────────────────────────────────────────────────────────────┐
│                        数据源 (Sources)                          │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐  │
│  │  Web    │ │ Mobile  │ │ Backend │ │  第三方 │ │  文件   │  │
│  │  埋点   │ │  埋点   │ │  日志   │ │  API    │ │  导入   │  │
│  └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘  │
└───────┼───────────┼───────────┼───────────┼───────────┼───────┘
        │           │           │           │           │
        └───────────┴───────────┴───────────┴───────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    数据采集层 (Collection)                       │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  SDK Collection Service (Node.js/Go)                     │   │
│  │  - 数据校验 │  - 数据清洗 │  - 数据脱敏 │  - 批量上报   │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    消息队列层 (Message Queue)                    │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  Apache Kafka                                             │   │
│  │  Topic: events-raw │ events-processed │ events-analytics │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    流处理层 (Stream Processing)                  │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  Apache Flink / Kafka Streams                            │   │
│  │  - 实时聚合 │ - 会话计算 │ - 异常检测 │ - 数据增强      │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    数据存储层 (Storage)                          │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  ClickHouse (主存储)                                      │   │
│  │  - 原始事件表 │ - 聚合表 │ - 物化视图 │ - 预聚合表       │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │  PostgreSQL (元数据)                                      │   │
│  │  - 用户表 │ - 项目表 │ - 事件定义 │ - 报表配置          │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │  Redis (缓存)                                             │   │
│  │  - 实时指标 │ - 会话状态 │ - 查询结果缓存                │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

### 3.2 ClickHouse 表结构设计

```sql
-- 原始事件表
CREATE TABLE events (
    event_id UUID,
    project_id UInt32,
    user_id String,
    anonymous_id String,
    event_name LowCardinality(String),
    event_time DateTime64(3),
    properties String, -- JSON
    context String,    -- JSON
    
    -- 系统字段
    received_at DateTime DEFAULT now(),
    
    INDEX idx_event_name event_name TYPE bloom_filter GRANULARITY 3,
    INDEX idx_user_id user_id TYPE bloom_filter GRANULARITY 3
) ENGINE = MergeTree()
PARTITION BY toYYYYMM(event_time)
ORDER BY (project_id, event_name, event_time)
TTL event_time + INTERVAL 1 YEAR;

-- 用户会话表
CREATE TABLE sessions (
    session_id UUID,
    project_id UInt32,
    user_id String,
    anonymous_id String,
    start_time DateTime64(3),
    end_time DateTime64(3),
    duration_ms UInt32,
    event_count UInt16,
    page_views UInt16,
    
    -- 会话属性
    referrer String,
    landing_page String,
    exit_page String,
    device_type LowCardinality(String),
    browser LowCardinality(String),
    os LowCardinality(String),
    country LowCardinality(String),
    
    INDEX idx_user_id user_id TYPE bloom_filter GRANULARITY 3
) ENGINE = MergeTree()
PARTITION BY toYYYYMM(start_time)
ORDER BY (project_id, start_time, user_id);

-- 预聚合日统计表
CREATE TABLE daily_stats (
    project_id UInt32,
    date Date,
    event_name LowCardinality(String),
    
    -- 统计指标
    total_count UInt64,
    unique_users UInt64,
    
    -- 按维度统计
    device_stats String, -- JSON
    country_stats String, -- JSON
    
    -- 计算时间
    calculated_at DateTime DEFAULT now()
) ENGINE = SummingMergeTree()
PARTITION BY toYYYYMM(date)
ORDER BY (project_id, date, event_name);
```

---

## 四、SDK 技术方案

### 4.1 JavaScript SDK 架构

```typescript
// 核心架构
interface AnalyticsSDK {
  // 初始化
  init(config: Config): void;
  
  // 事件跟踪
  track(event: string, properties?: object): void;
  
  // 用户识别
  identify(userId: string, traits?: object): void;
  
  // 页面自动跟踪
  page(name?: string, properties?: object): void;
  
  // 用户属性
  people: {
    set(properties: object): void;
    increment(property: string, value: number): void;
  };
}

// 加载方式
// 1. 标准加载
<script src="https://cdn.example.com/analytics.min.js"></script>
<script>
  analytics.init({
    projectId: 'YOUR_PROJECT_ID',
    trackPageView: true,
    trackClicks: true
  });
</script>

// 2. npm 安装
// npm install @startup-analytics/sdk
import { Analytics } from '@startup-analytics/sdk';
const analytics = new Analytics({ projectId: 'xxx' });
```

### 4.2 SDK 功能清单

| 功能 | Web SDK | iOS SDK | Android SDK | 服务端 SDK |
|------|---------|---------|-------------|------------|
| 事件追踪 | ✅ | ✅ | ✅ | ✅ |
| 用户识别 | ✅ | ✅ | ✅ | ✅ |
| 页面浏览 | ✅ | ✅ | ✅ | ❌ |
| 点击追踪 | ✅ | ❌ | ❌ | ❌ |
| 表单分析 | ✅ | ❌ | ❌ | ❌ |
| 会话录制 | ⚠️ | ⚠️ | ⚠️ | ❌ |
| 崩溃报告 | ❌ | ✅ | ✅ | ❌ |
| 离线缓存 | ✅ | ✅ | ✅ | N/A |

---

## 五、API 设计

### 5.1 REST API 规范

```yaml
# OpenAPI 3.0 规范
openapi: 3.0.0
info:
  title: Startup Analytics API
  version: 1.0.0

paths:
  /v1/track:
    post:
      summary: 上报事件
      requestBody:
        content:
          application/json:
            schema:
              type: object
              required: [event, project_id]
              properties:
                event:
                  type: string
                user_id:
                  type: string
                properties:
                  type: object
                timestamp:
                  type: string
                  format: date-time
      responses:
        200:
          description: 成功接收

  /v1/query/events:
    post:
      summary: 查询事件数据
      requestBody:
        content:
          application/json:
            schema:
              type: object
              properties:
                event_name:
                  type: string
                date_from:
                  type: string
                  format: date
                date_to:
                  type: string
                  format: date
                group_by:
                  type: array
                  items:
                    type: string
      responses:
        200:
          description: 查询结果
          content:
            application/json:
              schema:
                type: object
                properties:
                  data:
                    type: array
                  total:
                    type: integer

  /v1/funnels:
    get:
      summary: 获取漏斗分析
      parameters:
        - name: funnel_id
          in: query
          required: true
          schema:
            type: string
      responses:
        200:
          description: 漏斗数据
```

---

## 六、性能优化策略

### 6.1 查询优化

1. **预聚合**
   - 常用指标预计算
   - 物化视图
   - 增量聚合

2. **缓存策略**
   - Redis缓存热点数据
   - CDN缓存静态资源
   - 客户端缓存报表配置

3. **查询优化**
   - 限制查询时间范围
   - 采样查询（大数据量）
   - 异步查询（复杂报表）

### 6.2 写入优化

1. **批量写入**
   - SDK端批量上报
   - 服务端批量插入

2. **异步处理**
   - Kafka缓冲
   - 异步落库

3. **数据分区**
   - 按时间分区
   - 按项目分片

---

## 七、安全设计

### 7.1 数据安全

1. **传输安全**
   - 全站HTTPS
   - SDK上报TLS加密

2. **存储安全**
   - 敏感数据加密存储
   - 定期备份
   - 访问日志审计

3. **访问控制**
   - JWT认证
   - RBAC权限模型
   - API Key管理

### 7.2 隐私合规

1. **数据脱敏**
   - PII字段自动识别
   - 数据脱敏处理

2. **GDPR/CCPA支持**
   - 数据导出
   - 数据删除
   - 同意管理

3. **数据本地化**
   - 支持私有化部署
   - 数据不出境

---

## 八、扩展性设计

### 8.1 水平扩展

```
┌─────────────────────────────────────────────────────────────────┐
│                        Load Balancer                             │
└─────────────────────────────────────────────────────────────────┘
                              │
            ┌─────────────────┼─────────────────┐
            ▼                 ▼                 ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   API Server    │ │   API Server    │ │   API Server    │
│      Pod 1      │ │      Pod 2      │ │      Pod N      │
└─────────────────┘ └─────────────────┘ └─────────────────┘
            │                 │                 │
            └─────────────────┼─────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    ClickHouse Cluster                            │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐                           │
│  │ Shard 1 │ │ Shard 2 │ │ Shard N │                           │
│  │ Replica │ │ Replica │ │ Replica │                           │
│  └─────────┘ └─────────┘ └─────────┘                           │
└─────────────────────────────────────────────────────────────────┘
```

### 8.2 多租户架构

1. **逻辑隔离**
   - 项目ID作为所有表的分区键
   - 查询自动添加项目过滤

2. **资源隔离**
   - 按项目限流
   - 资源配额管理

---

*文档持续更新中...*
