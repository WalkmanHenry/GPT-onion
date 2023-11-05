# 📑 附录4.代码目录表

## 后端代码目录结构表:



```
├── api // API接口
│   └── v1 // v1版本API
├── config // 配置
├── core // 核心组件
├── docs // 文档
├── global // 全局对象
├── initialize // 初始化
│   └── internal // 内部初始化函数
├── middleware // 中间件
├── model // 模型
│   ├── request // 请求参数结构体
│   └── response // 响应结构体 
├── packfile // 打包文件
├── resource // 资源
│   ├── excel // Excel文件
│   ├── page // 页面文件
│   └── template // 模板
├── router // 路由
├── service // 业务逻辑
├── source // 源数据函数
└── utils // 工具函数
    ├── timer // 定时器封装
    └── upload // 上传封装
```



| 文件夹          | 说明            | 描述                                                |
| ------------ | ------------- | ------------------------------------------------- |
| `api`        | api层          | api层                                              |
| `--v1`       | v1版本接口        | v1版本接口                                            |
| `config`     | 配置包           | config.yaml对应的配置结构体                               |
| `core`       | 核心文件          | 核心组件(zap, viper, server)的初始化                      |
| `docs`       | swagger文档目录   | swagger文档目录                                       |
| `global`     | 全局对象          | 全局对象                                              |
| `initialize` | 初始化           | router,redis,gorm,validator, timer的初始化            |
| `--internal` | 初始化内部函数       | gorm 的 longger 自定义,在此文件夹的函数只能由 `initialize` 层进行调用 |
| `middleware` | 中间件层          | 用于存放 `gin` 中间件代码                                  |
| `model`      | 模型层           | 模型对应数据表                                           |
| `--request`  | 入参结构体         | 接收前端发送到后端的数据。                                     |
| `--response` | 出参结构体         | 返回给前端的数据结构体                                       |
| `packfile`   | 静态文件打包        | 静态文件打包                                            |
| `resource`   | 静态资源文件夹       | 负责存放静态文件                                          |
| `--excel`    | excel导入导出默认路径 | excel导入导出默认路径                                     |
| `--page`     | 表单生成器         | 表单生成器 打包后的dist                                    |
| `--template` | 模板            | 模板文件夹,存放的是代码生成器的模板                                |
| `router`     | 路由层           | 路由层                                               |
| `service`    | service层      | 存放业务逻辑问题                                          |
| `source`     | source层       | 存放初始化数据的函数                                        |
| `utils`      | 工具包           | 工具函数封装                                            |
| `--timer`    | timer         | 定时器接口封装                                           |
| `--upload`   | oss           | oss接口封装                                           |
