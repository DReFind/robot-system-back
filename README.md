# Robot System Back - 机器人产品售卖系统后端

## 项目简介

本项目是一个基于 Spring Boot 框架的机器人产品售卖系统后端服务，为前端提供完整的 RESTful API 接口支持。系统涵盖用户认证、商品管理、订单处理、文件存储等核心功能，可作为毕业设计项目或实际商业应用的后端解决方案。

## 技术栈

| 类别 | 技术 | 版本 |
|------|------|------|
| 编程语言 | Java | 17 | 
| 核心框架 | Spring Boot | 4.0.8 |
| 数据库 | MySQL | 8.x |
| ORM 框架 | MyBatis-Plus | 3.5.15 |
| API 文档 | Knife4j / SpringDoc | 4.4.0 |
| 对象存储 | MinIO | - |
| 身份认证 | JWT | - |
| 简化开发 | Lombok | - |
| 构建工具 | Maven | - |

## 核心功能

- **用户管理**：用户注册、登录、JWT Token 认证与权限控制
- **商品管理**：机器人商品的增删改查、分类管理、上下架操作
- **订单管理**：订单创建、支付流程、订单状态管理
- **文件存储**：基于 MinIO 的文件上传与下载服务
- **API 文档**：集成 Knife4j，提供交互式 API 文档，便于接口调试

## 项目结构

```
robot-system-back/
├── src/
│   ├── main/
│   │   ├── java/robot/systemback/
│   │   │   └── RobotSystemBackApplication.java   # 启动类
│   │   └── resources/
│   │       ├── application.yml                   # 应用配置文件
│   │       ├── logback.xml                       # 日志配置
│   │       └── static/
│   │           └── index.html                    # 默认欢迎页
│   └── test/                                     # 单元测试目录
├── pom.xml                                       # Maven 依赖配置
└── README.md                                     # 项目说明文档
```

## 快速开始

### 环境要求

- **JDK**：17 及以上版本
- **Maven**：3.8 及以上版本
- **MySQL**：8.0 及以上版本
- **MinIO**（可选）：用于文件上传存储功能

### 1. 获取项目

```bash
git clone <repository-url>
cd robot-system-back
```

### 2. 数据库初始化

创建数据库并设置编码：

```sql
CREATE DATABASE robot_system DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### 3. 修改配置

编辑 `src/main/resources/application.yml`，修改数据库连接信息：

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/robot_system
    username: 
    password: 
    driver-class-name: 
```

如需文件上传功能，请配置 MinIO：

```yaml
minio:
  url: http://your-minio-server:9090
  access-key: your-access-key
  secret-key: your-secret-key
  bucket-name: your-bucket
```

### 4. 编译运行

```bash
# 编译项目
mvn clean compile

# 启动项目
mvn spring-boot:run

# 打包构建
mvn clean package
```

### 5. 访问服务

| 服务 | 地址 |
|------|------|
| 应用首页 | http://localhost:8080 |
| Knife4j 文档 | http://localhost:8080/doc.html |
| Swagger UI | http://localhost:8080/swagger-ui.html |

## 配置说明

### JWT 令牌配置

```yaml
sky:
  jwt:
    admin-secret-key: your-secret-key   # JWT 签名密钥（请修改为安全值）
    admin-ttl: 720000000                # 令牌有效期（单位：毫秒）
    admin-token-name: token             # HTTP 请求头中的令牌名称
```

### MyBatis-Plus 配置

```yaml
mybatis-plus:
  configuration:
    map-underscore-to-camel-case: true   # 开启下划线转驼峰映射
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl  # SQL 日志输出
  mapper-locations: classpath*:mapper/**/*.xml  # Mapper XML 文件路径
```

## 开发指南

### 新增业务模块

1. 在 `controller` 包下创建控制器类，添加 `@RestController` 注解
2. 使用 `@Operation`、`@Tag` 等 Knife4j 注解完善接口文档描述
3. 在 `service` 包下编写业务逻辑层代码
4. 在 `mapper` 包下编写数据访问接口及 XML 映射文件

### API 文档调试

项目已集成 Knife4j 接口文档工具：

- 访问地址：`http://localhost:8080/doc.html`
- 支持在线接口测试、请求参数查看、响应示例展示等

## 许可证

本项目仅供学习和毕业设计使用。