# 📗 附录2.数据字典

## 数据字典

> 本字典仅为演示业务逻辑和项目管理中所需要涉及的业务步骤，实际生产环境更加复杂，详见项目代码。

#### 1. 用户表（users）

| 字段名         | 数据类型    | 长度  | 主键 | 是否可空 | 默认值 | 描述      |
| ----------- | ------- | --- | -- | ---- | --- | ------- |
| user\_id    | INT     |     | 是  | 否    |     | 用户ID    |
| username    | VARCHAR | 50  |    | 否    |     | 用户名     |
| password    | VARCHAR | 64  |    | 否    |     | 密码（哈希值） |
| email       | VARCHAR | 50  |    | 是    |     | 邮箱      |
| avatar      | VARCHAR | 255 |    | 是    |     | 头像链接    |
| created\_at | INT     | 10  |    | 否    |     | 创建时间    |
| updated\_at | INT     | 10  |    | 否    |     | 更新时间    |

#### 2. 提示词表（prompts）

| 字段名         | 数据类型    | 长度  | 主键 | 是否可空 | 默认值 | 描述    |
| ----------- | ------- | --- | -- | ---- | --- | ----- |
| prompt\_id  | INT     |     | 是  | 否    |     | 提示词ID |
| creator\_id | INT     |     |    | 否    |     | 创建者ID |
| title       | VARCHAR | 100 |    | 否    |     | 提示词标题 |
| description | TEXT    |     |    | 是    |     | 提示词描述 |
| prompt      | TEXT    |     |    | 否    |     | 提示词内容 |
| created\_at | INT     | 10  |    | 否    |     | 创建时间  |
| updated\_at | INT     | 10  |    | 否    |     | 更新时间  |

#### 3. 评论表（comments）

| 字段名         | 数据类型 | 长度 | 主键 | 是否可空 | 默认值 | 描述    |
| ----------- | ---- | -- | -- | ---- | --- | ----- |
| comment\_id | INT  |    | 是  | 否    |     | 评论ID  |
| prompt\_id  | INT  |    |    | 否    |     | 提示词ID |
| user\_id    | INT  |    |    | 否    |     | 用户ID  |
| text        | TEXT |    |    | 否    |     | 评论内容  |
| created\_at | INT  | 10 |    | 否    |     | 创建时间  |

#### 4. 评分表（ratings）

| 字段名         | 数据类型     | 长度 | 主键 | 是否可空 | 默认值 | 描述    |
| ----------- | -------- | -- | -- | ---- | --- | ----- |
| rating\_id  | INT      |    | 是  | 否    |     | 评分ID  |
| prompt\_id  | INT      |    |    | 否    |     | 提示词ID |
| user\_id    | INT      |    |    | 否    |     | 用户ID  |
| rating      | SMALLINT |    |    | 否    |     | 评分值   |
| created\_at | INT      | 10 |    | 否    |     | 创建时间  |

#### 5. 精选集表（collections）

| 字段名            | 数据类型      | 长度  | 主键 | 是否可空 | 默认值 | 描述     |
| -------------- | --------- | --- | -- | ---- | --- | ------ |
| collection\_id | INT       |     | 是  | 否    |     | 精选集ID  |
| creator\_id    | INT       |     |    | 否    |     | 创建者ID  |
| title          | VARCHAR   | 100 |    | 否    |     | 精选集标题  |
| description    | TEXT      |     |    | 是    |     | 精选集描述  |
| cover\_image   | VARCHAR   | 255 |    | 是    |     | 封面图片链接 |
| created\_at    | TIMESTAMP |     |    | 否    |     | 创建时间   |
| updated\_at    | TIMESTAMP |     |    | 否    |     | 更新时间   |

#### 6. 精选集提示词关联表（collection\_prompts）

| 字段名                    | 数据类型 | 长度 | 主键 | 是否可空 | 默认值 | 描述    |
| ---------------------- | ---- | -- | -- | ---- | --- | ----- |
| collection\_prompt\_id | INT  |    | 是  | 否    |     | 关联ID  |
| collection\_id         | INT  |    |    | 否    |     | 精选集ID |
| prompt\_id             | INT  |    |    | 否    |     | 提示词ID |

#### 7. 用户精选集关联表（user\_collections）

| 字段名                  | 数据类型 | 长度 | 主键 | 是否可空 | 默认值 | 描述    |
| -------------------- | ---- | -- | -- | ---- | --- | ----- |
| user\_collection\_id | INT  |    | 是  | 否    |     | 关联ID  |
| user\_id             | INT  |    |    | 否    |     | 用户ID  |
| collection\_id       | INT  |    |    | 否    |     | 精选集ID |
