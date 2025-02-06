# DifyTimeTask 定时任务插件

## 简介

DifyTimeTask 是一个基于 Python 的定时任务插件，修改自原脚本 https://github.com/haikerapples/timetask 作用在帮助用户通过简单的指令创建、管理和执行定时任务。该插件支持多种任务类型，包括个人任务、群任务、GPT 任务等，并且可以通过 Excel 文件持久化存储任务数据。插件还支持任务的延时执行、任务列表查看、任务取消等功能。

## 修正说明
2025年2月6日：
添加任务时可以使用更灵活的时间格式，而不必严格遵守 HH:mm 的格式。
输入 9:2 会被格式化为 09:02:00。
输入 20:1 会被格式化为 20:01:00。

2025年1月15日：
修正 difytimetask 插件在处理其特定命令时检查管理员权限，会影响其他插件的正常运行问题。


## 插件环境

此插件只能在 https://github.com/hanfangyuan4396/dify-on-wechat 下运行。

插件存放路径：dify-on-wechat/plugins/difytimetask

#### 亮点功能

1. **多任务类型支持**：
   - 支持个人任务、群任务、GPT 任务等多种任务类型，满足不同场景的需求。

2. **任务持久化**：
   - 任务数据通过 Excel 文件存储，支持任务的持久化和历史任务的管理，确保任务数据不会丢失。

3. **延时任务**：
   - 支持为任务设置延时区间，任务会在指定时间范围内随机延时执行，避免任务执行时间过于集中。

4. **灵活的周期设置**：
   - 支持多种周期设置，如每天、每周、工作日、具体日期等，满足不同周期的任务需求。

5. **Cron 表达式支持**：
   - 支持使用 Cron 表达式来定义复杂的任务执行时间，适合需要精确控制的定时任务。

6. **管理员认证**：
   - 只有通过管理员认证的用户才能使用插件的功能，确保任务管理的安全性。

7. **任务列表查看与取消**：
   - 支持查看当前任务列表和取消指定任务，方便用户管理任务。


## 功能特性

- **定时任务创建**：支持通过指令创建定时任务，任务可以指定时间、周期、事件内容等。
- **任务类型**：支持个人任务、群任务、GPT 任务等多种任务类型。
- **任务管理**：支持查看任务列表、取消任务、取消所有任务等功能。
- **任务延时**：支持为任务设置延时区间，任务会在指定时间范围内随机延时执行。
- **任务持久化**：任务数据通过 Excel 文件存储，支持任务的持久化和历史任务的管理。
- **多平台支持**：目前只支持 dify-on-wechat 项目。

## 使用注意事项

### 1. 插件依赖 Godcmd 认证
本插件需要结合 **Godcmd 认证** /plugins/godcmd 文件使用。只有通过认证的管理员用户才能使用插件的功能。请确保在 `global_config` 中正确配置管理员用户列表。

### 2. 群任务定时限制
在对群聊进行定时任务设置时，**目标群聊必须保存到通讯录中**。也就是说，只有那些在群信息中勾选了“保存到通讯录”的群聊才能被插件识别并用于定时任务。如果群聊未保存到通讯录，插件将无法找到对应的群 ID，导致任务设置失败。

### 3. 个人任务定时限制
在对个人用户进行定时任务设置时，**目标用户必须是您的好友**。只有已添加为好友的用户才能被插件识别并用于定时任务。如果目标用户未添加为好友，插件将无法找到对应的用户 ID，导致任务设置失败。

### 4. 其他注意事项
- 请确保插件的配置文件 `config.json` 正确填写了 Gewechat 的相关信息（如 `gewechat_app_id`、`gewechat_base_url` 和 `gewechat_token`）。
- 定时任务的执行依赖于系统时间，请确保运行插件的服务器或设备时间准确。
- 如果任务执行失败，请检查日志文件以获取更多错误信息。


## 安装与配置

### 依赖安装

在运行该插件之前，请确保已安装以下依赖：

```bash
pip install arrow>=1.2.3
pip install openpyxl>=3.1.2
pip install croniter>=1.4.1
```

### 配置文件

插件依赖dify-on-wechat  `config.json` 文件进行配置，配置文件应位于项目的根目录下。配置文件内容如下：

```json
{
  "gewechat_app_id": "your_app_id",
  "gewechat_base_url": "your_base_url",
  "gewechat_token": "your_token"
}
```

- `gewechat_app_id`：Gewechat 应用的 ID。
- `gewechat_base_url`：Gewechat 的基础 URL。
- `gewechat_token`：Gewechat 的认证 Token。



## 使用说明

### 添加定时任务

通过以下指令格式添加定时任务：

```
$time 周期 时间 事件 延时时间
```

- **周期**：任务的执行周期，支持 `今天`、`明天`、`后天`、`每天`、`每周X`、`YYYY-MM-DD` 等格式。
- **时间**：任务的执行时间，支持 `HH:mm:ss` 或 `X点X分` 格式。
- **事件**：任务的具体内容，可以是提醒、GPT 任务等。
- **延时时间**：任务延时执行时间，会自动进位。
- 
**示例**：

- 添加一个今天 10:00 的提醒任务：
  ```
  $time 今天 10:00 提醒我健身
  ```

- 添加一个每天 10:00 的 GPT 任务：
  ```
  $time 每天 10:00 GPT 夸夸我
  ```

- 添加一个每周三 10:00 的群任务：
  ```
  $time 每周三 10:00 提醒我开会 group[工作群]
  ```
- 添加一个每周三 10:00 的对个人任务：
  ```
  $time 每周三 10:00 提醒我开会 user[用户昵称]
  ```
- 组合方式很多：
  ```
  $time 每周三 10:00 提醒我开会 user[用户昵称] t[1-60]
  ```
  ```
  $time 每周三 10:00 GPT 下班了，该回家了 user[用户昵称] t[1-60]
  ```
  
### 查看任务列表

通过以下指令查看当前的任务列表：

```
$time 任务列表
```

### 取消任务

通过以下指令取消指定任务：

```
$time 取消任务 任务编号
```

- **任务编号**：任务编号可以在添加任务成功时获取，或者在任务列表中查看。

### 取消所有任务

通过以下指令取消所有任务：

```
$time 取消所有任务
```

### 延时任务

在任务内容中添加 `t[1-3]` 表示任务的延时区间为 1 到 3 分钟。任务会在指定时间范围内随机延时执行。

**示例**：

```
$time 今天 10:00 提醒我健身 t[1-3]
```

### 示例截图

![取消所有任务](https://github.com/cm04918/difytimetask/blob/main/images/取消所有任务_20250114094623.png) 
![群轮询任务](https://github.com/cm04918/difytimetask/blob/main/images/群轮询任务_20250114145728.png) 
![延时服务](https://github.com/cm04918/difytimetask/blob/main/images/延时服务_20250114145219.png)
![延时轮询任务](https://github.com/cm04918/difytimetask/blob/main/images/延时轮询任务_20250114145843.png)
![延时群任务](https://github.com/cm04918/difytimetask/blob/main/images/延时群任务_20250114094258.png)

### 任务模型

任务模型 `TimeTaskModel` 定义了任务的基本属性，包括任务 ID、时间、周期、事件内容等。任务模型还提供了任务的状态管理、时间计算等功能。

### Excel 文件操作

任务数据通过 Excel 文件进行存储，Excel 文件默认名称为 `timeTask.xlsx`，包含两个 Sheet：

- **定时任务**：存储当前有效的定时任务。
- **历史任务**：存储已过期或已取消的任务。

## 注意事项

1. **管理员认证**：只有通过管理员认证的用户才能使用该插件的功能。管理员用户需要在 `global_config` 中配置。
2. **任务持久化**：任务数据通过 Excel 文件存储，请确保插件有权限读写该文件。
3. **任务延时**：延时任务的执行时间会在指定范围内随机生成，确保任务的执行时间不会过于集中。

## 示例

### 添加任务

```bash
$time 今天 10:00 提醒我健身
```

### 查看任务列表

```bash
$time 任务列表
```

### 取消任务

```bash
$time 取消任务 urwOi0he
```

### 取消所有任务

```bash
$time 取消所有任务
```

## 贡献与反馈
经过几天的反复修改和调试，我终于理清了各个模块的工作原理，并成功实现了插件的核心功能。

## 支持与打赏
如果这个项目对你有帮助，欢迎请我喝杯咖啡 ☕️，支持我继续开发和完善！

![微信打赏](https://github.com/cm04918/difytimetask/blob/main/images/20250114092342.png)

感谢你的支持！❤️
---

感谢您使用 DifyTimeTask 插件！希望它能为您的工作和生活带来便利。
