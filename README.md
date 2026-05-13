# Spring Lib Parent

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Maven Central](https://img.shields.io/badge/Maven-GitHub%20Packages-red.svg)](https://github.com/boge-mvp/spring-lib-parent)

一个基于 **Spring Boot 3.3.2** + **Kotlin 2.0.0** 的 Maven Parent POM 项目，为子项目提供统一的依赖版本管理和标准化构建配置。

## 📋 项目概述

本项目是一个 **Maven Parent POM**（打包类型为 `pom`），不包含业务代码，主要提供：

- ✅ **统一依赖管理**：集中管理 Spring Boot、Kotlin、MyBatis Plus 等常用库的版本
- ✅ **标准化构建配置**：预配置的 Maven 插件和编译参数
- ✅ **多 Profile 支持**：按需激活不同功能模块（MySQL、Redis、分布式锁等）
- ✅ **Kotlin 集成**：完整的 Kotlin + Spring Boot 开发支持
- ✅ **JDK 21 优化**：针对 JDK 21 的 ZGC 和模块化配置

## 🚀 快速开始

### 1. 配置 Maven 仓库

在子项目的 `pom.xml` 中添加 GitHub Packages 仓库配置：

```xml
<repositories>
    <repository>
        <id>github-spring-lib-parent</id>
        <url>https://maven.pkg.github.com/boge-mvp/repo</url>
    </repository>
</repositories>
```

或者在 `~/.m2/settings.xml` 中全局配置：

```xml
<settings>
    <profiles>
        <profile>
            <id>github-repo</id>
            <repositories>
                <repository>
                    <id>github-spring-lib-parent</id>
                    <url>https://maven.pkg.github.com/boge-mvp/repo</url>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                </repository>
            </repositories>
        </profile>
    </profiles>
    <activeProfiles>
        <activeProfile>github-repo</activeProfile>
    </activeProfiles>
</settings>
```

### 2. 添加 Parent 依赖

在你的 Spring Boot 项目的 `pom.xml` 中添加：

```xml
<parent>
    <groupId>com.boge.spring.parent</groupId>
    <artifactId>spring-lib-parent</artifactId>
    <version>1.5.0</version>
</parent>
```

### 3. 激活 Profile（可选）

然后根据需要激活相应的 Profile：

```xml
<profiles>
    <!-- 使用 MySQL + MyBatis Plus -->
    <profile>
        <id>XSpringBootMysql</id>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    
    <!-- 使用 Redis -->
    <profile>
        <id>XSpringBootRedis</id>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
</profiles>
```

## 📦 技术栈

| 技术 | 版本 | 说明 |
|------|------|------|
| Spring Boot | 3.3.2 | Web 框架 |
| Kotlin | 2.0.0 | 编程语言 |
| JDK | 21 | Java 运行环境 |
| MyBatis Plus | 3.5.7 | ORM 框架 |
| MySQL Connector | 9.0.0 | 数据库驱动 |
| Druid | 1.2.23 | 数据库连接池 |
| Redis | - | 缓存中间件 |
| ShedLock | 5.14.0 | 分布式锁 |
| Retrofit2 | 2.11.0 | HTTP 客户端 |
| OkHttp | 5.0.0-alpha.14 | HTTP 客户端 |

## 🔧 可用 Profile

### 核心 Profile（默认激活）

| Profile ID | 功能 | 说明 |
|-----------|------|------|
| `XKotlin` | Kotlin 支持 | Kotlin 编译和序列化支持 |
| `XJava` | Java 支持 | Java 编译支持 |
| `XSpringBoot` | Spring Boot 基础 | Web、AOP、Validation、Log4j2 |

### 数据库相关

| Profile ID | 功能 | 包含组件 |
|-----------|------|---------|
| `XSpringBootMysql` | MySQL 支持 | JPA、MySQL Driver、Druid、MyBatis Plus |
| `XMyBatisPlugDynamicData` | 动态数据源 | Dynamic Datasource |
| `XSpringBootRedis` | Redis 支持 | Spring Data Redis |

### 分布式锁

| Profile ID | 功能 | 存储方式 |
|-----------|------|---------|
| `XShedlockSpringRedis` | 分布式锁 | Redis |
| `XShedlockSpringMysql` | 分布式锁 | MySQL |

### 监控与管理

| Profile ID | 功能 | 说明 |
|-----------|------|------|
| `XActuatorServer` | Actuator 服务端 | Spring Boot Admin Server |
| `XActuatorClient` | Actuator 客户端 | Spring Boot Admin Client |

### HTTP 客户端

| Profile ID | 功能 | 说明 |
|-----------|------|------|
| `XRetrofit` | Retrofit | 类型安全的 HTTP 客户端 |
| `XOKHttp` | OkHttp | HTTP 客户端 |

### 构建工具

| Profile ID | 功能 | 说明 |
|-----------|------|------|
| `XPlugProtobuf` | Protobuf | Protocol Buffers 编译支持 |
| `XPlugSpringSeparateLib` | 分离打包 | JAR 与依赖分离打包 |
| `XPlugSpringBootBuild` | 完整打包 | 标准 Spring Boot 打包 |
| `XPlugDocsBuild` | 文档生成 | Dokka 文档生成 |
| `XPlugSourcesBuild` | 源码包 | 生成 sources.jar |
| `XGenerateYmlConfig` | 配置元数据 | YAML 配置提示生成 |
| `XCompileTest` | 测试编译 | 启用测试编译 |

## 💡 使用示例

### 示例 1：Web 项目 + MySQL + Redis

```xml
<parent>
    <groupId>com.boge.spring.parent</groupId>
    <artifactId>spring-lib-parent</artifactId>
    <version>1.5.0</version>
</parent>

<profiles>
    <profile>
        <id>XSpringBootMysql</id>
        <activation><activeByDefault>true</activeByDefault></activation>
    </profile>
    <profile>
        <id>XSpringBootRedis</id>
        <activation><activeByDefault>true</activeByDefault></activation>
    </profile>
</profiles>
```

### 示例 2：微服务项目 + 分布式锁

```xml
<parent>
    <groupId>com.boge.spring.parent</groupId>
    <artifactId>spring-lib-parent</artifactId>
    <version>1.5.0</version>
</parent>

<profiles>
    <profile>
        <id>XSpringBootMysql</id>
        <activation><activeByDefault>true</activeByDefault></activation>
    </profile>
    <profile>
        <id>XShedlockSpringMysql</id>
        <activation><activeByDefault>true</activeByDefault></activation>
    </profile>
    <profile>
        <id>XActuatorClient</id>
        <activation><activeByDefault>true</activeByDefault></activation>
    </profile>
</profiles>
```

### 示例 3：纯 Kotlin 项目

```xml
<parent>
    <groupId>com.boge.spring.parent</groupId>
    <artifactId>spring-lib-parent</artifactId>
    <version>1.5.0</version>
</parent>

<!-- XKotlin 和 XSpringBoot 默认已激活，无需额外配置 -->
```

## 🏗️ 构建与发布

### 本地构建

```bash
# 基本构建
mvn clean install

# 生成源码和文档
mvn clean install -P XPlugSourcesBuild,XPlugDocsBuild

# 指定版本号
mvn clean install -Dproject.version=1.5.0
```

### CI/CD 自动化发布

项目已配置 GitHub Actions，推送 tag 自动触发发布：

```bash
# 创建并推送 tag
git tag v1.5.0
git push origin v1.5.0
```

GitHub Actions 会自动：
1. 提取版本号（去除 `v` 前缀）
2. 执行 Maven Install
3. 生成 POM、源码包、文档包
4. 发布到 GitHub Packages

## 📂 项目结构

```
spring-lib-parent/
├── pom.xml                    # Parent POM 配置
├── .github/workflows/         # GitHub Actions 配置
│   └── publish.yml           # 发布工作流
├── src/main/
│   ├── java/                  # Java 源码目录（可选）
│   └── kotlin/                # Kotlin 源码目录（可选）
├── deploy/                    # 构建输出目录
│   └── lib/                   # 依赖库目录
└── README.md                  # 项目说明文档
```

## ⚙️ 核心配置

### JVM 参数

```properties
-Dfile.encoding=UTF-8
-XX:+UseZGC
--add-opens java.base/java.lang.invoke=ALL-UNNAMED
--add-opens java.base/java.lang.reflect=ALL-UNNAMED
# ... 更多 module opens 配置
```

### 编译配置

- **Java 版本**: 21
- **Kotlin 版本**: 2.0.0
- **编码**: UTF-8
- **测试**: 默认跳过（`-Dmaven.test.skip=true`）

## 📝 版本历史

### v1.5.0 (当前版本)
- 升级到 Spring Boot 3.3.2
- 升级到 Kotlin 2.0.0
- 升级到 JDK 21
- 优化 Profile 配置
- 添加 GitHub Actions CI/CD 支持

### v1.x.x
- 初始版本发布
- 支持 Spring Boot 3.x
- 集成 Kotlin 支持
- 提供多种数据库和中间件 Profile

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

本项目采用 Apache License 2.0 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 📧 联系方式

- **Group ID**: `com.boge.spring.parent`
- **Artifact ID**: `spring-lib-parent`
- **GitHub Repository**: [https://github.com/boge-mvp/spring-lib-parent](https://github.com/boge-mvp/spring-lib-parent)

> **注意**: 使用前请确保已配置 GitHub Packages Maven 仓库地址

---

**Made with ❤️ using Spring Boot & Kotlin**
