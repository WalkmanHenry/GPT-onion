# 📕 附录2.GPT-Onion技术文档

## GPT-Onion技术文档

### 1. 项目概述

#### 1.1 项目背景

GPT-Onion是一个以社区为中心的平台，旨在通过AI提示词来帮助用户学习、构建和展示AI功能。

#### 1.2 功能需求

{% content-ref url="appendix-1.gptonion-prd.md" %}
[appendix-1.gptonion-prd.md](appendix-1.gptonion-prd.md)
{% endcontent-ref %}

#### 1.3 用户角色

[#yong-hu-jiao-se](appendix-1.gptonion-prd.md#yong-hu-jiao-se "mention")(参见产品需求文档)

### 2. 技术架构

#### 2.1 前后端技术栈

* 前端: Javascript, Vue 3(Node.js)
* 后端: Golang,Gin,gorm
* 使用Gin-Vue-Admin框架

#### 2.2 数据库设计

* 数据库: MySQL (InnoDB)
* 缓存: Redis

{% content-ref url="appendix-3-data-dict.md" %}
[appendix-3-data-dict.md](appendix-3-data-dict.md)
{% endcontent-ref %}

#### 2.3 错误处理和日志记录

* 错误代码规范: HTTP状态码
* 日志记录: 使用go-log库进行日志记录

### 3. 开发环境和工具

#### 3.1 开发环境配置

* 版本控制: Git (GitHub)
* 推荐编辑器/IDE: Vim / Goland / Intelli J
* Golang version: ^go1.20.4
* MySQL: ^8.0
* Node.js:^20.8



#### 3.2 代码版本控制和分支策略

* 主分支: main
* 开发分支: dev
* 功能分支: feature/\<feature-name>

#### 3.3 项目构建和部署

* 本地开发环境: Docker Compose
* 生产环境部署: AWS EC2实例

### 4. 测试策略

#### 4.1 单元测试

**4.1.1 为什么进行单元测试**

单元测试主要用于验证代码中的各个单元（如函数或方法）是否按照预期工作。这有助于及时发现代码中的错误，减少系统中的缺陷，并提高代码质量。

**4.1.2 如何进行单元测试**

使用Go的内置`testing`包进行单元测试。每个测试函数都以`Test`开头，并接受一个`*testing.T`类型的参数。

**示例**:

```go
func TestAdd(t *testing.T) {
    result := Add(2, 3)
    if result != 5 {
        t.Errorf("Expected 5, but got %d", result)
    }
}
```

运行单元测试:

```bash
go test ./...
```

#### 4.2 集成测试

**4.2.1 为什么进行集成测试**

集成测试是为了验证不同模块或服务之间的交互是否按预期工作。特别是在微服务或分层架构中，这种测试确保了整个系统的连续性和一致性。

**4.2.2 如何进行集成测试**

使用Postman进行API集成测试:

1. **创建一个新的请求**: 在Postman中，点击“新建”按钮创建一个新的HTTP请求。
2. **设置请求参数**: 根据API的要求，设置相应的HTTP方法、URL、参数、请求体和头部。
3. **发送请求**: 点击“发送”按钮执行请求。
4. **检查响应**: 根据预期结果验证响应的状态码、头部和响应体。

#### 4.3 性能测试

**4.3.1 为什么进行性能测试**

性能测试是为了确保系统在预期负载和超出预期负载时都能正常工作。这有助于识别系统的瓶颈，优化性能，并确保系统在高负载时的稳定性。

**4.3.2 如何进行性能测试**

使用JMeter进行性能测试:

1. **创建一个新的测试计划**: 在JMeter中，选择“文件” > “新建”创建一个新的测试计划。
2. **添加线程组**: 右键点击测试计划，选择“添加” > “线程组”。设置线程数、循环次数等参数。
3. **添加HTTP请求**: 右键点击线程组，选择“添加” > “取样器” > “HTTP请求”。设置服务器名称或IP、路径、方法等。
4. **运行测试**: 点击“运行”按钮开始执行性能测试。
5. **查看结果**: 添加结果树和图表监听器以可视化测试结果。

### 5. 项目里程碑和时间线

(基于3天的开发时间，需要进一步确定里程碑和时间线)

### 6. API设计和文档

#### 6.1 API命名和结构: RESTful API

RESTful API设计基于HTTP方法，主要包括GET、POST、PUT、DELETE等，以及清晰的URL资源标识。

**示例**:

* 获取所有提示词: `GET /prompts`
* 获取特定提示词: `GET /prompts/{id}`
* 创建新提示词: `POST /prompts`
* 更新提示词: `PUT /prompts/{id}`
* 删除提示词: `DELETE /prompts/{id}`

#### 6.2 API文档: 使用Swagger生成API文档

**6.2.1 为什么使用Swagger**

* **自动生成**：基于代码中的注释自动生成API文档。
* **交互性**：允许开发人员和使用者通过Swagger UI直接在浏览器中与API进行交互。
* **兼容性**：支持多种语言和工具。

**6.2.2 为API编写注释**

在每个API的上方编写适当的注释，例如：

```go
// @Summary Get all prompts
// @Description Get all prompts from database
// @Tags Prompts
// @Accept  json
// @Produce  json
// @Success 200 {array} Prompts
// @Router /prompts [get]
```

### 7. 系统维护

#### 7.1 定期备份

**目标**: 确保在任何故障或数据损失的情况下，都能迅速恢复到一个稳定的状态。

**执行步骤**:

1. **数据库备份**:
   * 定时任务: 使用`cron`或相似工具每日执行备份任务。
   * 工具: `mysqldump`或`Percona XtraBackup`。
   * 存储: 将备份保存到一个与生产环境分离的位置，如云存储或物理不同的备份服务器。
   * 测试: 每月进行一次恢复测试，确保备份文件有效。
2. **代码备份**:
   * 通过Git进行版本控制，确保所有更改都被提交和推送到远程仓库。
   * 定期将远程仓库的备份存储到另一个地方，以防原存储地点出现问题。

#### 7.2 更新和补丁

**目标**: 保持系统、库和所有依赖的最新状态，确保安全和性能。

**执行步骤**:

1. **监测更新**:
   * 使用工具如`go list -u -m all`检查Golang的依赖更新。
   * 为操作系统和中间件配置自动更新通知。
2. **应用更新**:
   * 在测试环境中首先应用所有更新。
   * 进行回归测试，确保更新不会引入新的问题。
   * 在验证后，将更新部署到生产环境。
3. **安全补丁**:
   * 关注Golang、Gin、gorm以及其他主要依赖的安全通告。
   * 尽快应用任何安全补丁。

#### 7.3 容量规划

**目标**: 预测和应对未来的增长，避免因超出资源限制而导致的系统故障。

**执行步骤**:

1. **监控资源使用**:
   * 使用工具如`htop`, `iostat`, `netstat`等来监控CPU、内存、磁盘和网络的使用情况。
   * 监控数据库的大小和查询性能。
2. **预测增长**:
   * 根据过去的数据，预测未来的流量和数据增长。
   * 为可能的流量高峰进行规划，如促销活动或特定事件。
3. **扩展资源**:
   * 如果预测的增长接近当前的资源限制，考虑进行垂直或水平扩展。
   * 定期清理和优化数据库，如删除旧数据和重新索引。

每个步骤都需要定期审查和调整，确保其持续符合项目的需要。

### 8. 团队协作和代码审查

* 团队协作工具: GitHub Projects
* 代码审查流程: GitHub Pull Requests
