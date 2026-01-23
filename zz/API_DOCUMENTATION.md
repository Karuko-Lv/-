# 项目API文档

## 1. 概述

本项目提供了一套完整的设备管理API，用于监控和控制各种环境监测设备。API采用RESTful设计风格，通过HTTP协议进行通信，支持设备的连接、断开和状态查询等操作。

## 2. 基础信息

### 2.1 服务器地址

默认情况下，服务器运行在本地端口8080（具体端口可能根据配置有所不同）。

### 2.2 响应格式

所有API响应均采用JSON格式，包含以下基本字段：

- `success`：布尔值，表示操作是否成功
- `message`：字符串，描述操作结果
- `deviceId`：字符串，仅在操作指定设备时返回，标识设备ID

### 2.3 错误处理

API使用HTTP状态码来表示请求的处理结果：

- `200 OK`：请求成功
- `400 Bad Request`：请求参数错误
- `500 Internal Server Error`：服务器内部错误

## 3. API端点

### 3.1 根路径

**路径**：`/`

**方法**：`GET`

**描述**：返回简单的问候消息，用于测试服务器是否正常运行。

**响应**：

```
Hello, HTTP Server!
```

### 3.2 连接所有设备

**路径**：`/api/devices/connect-all`

**方法**：`POST`

**描述**：尝试连接所有已注册的设备。

**请求体**：无

**响应**：

成功：
```json
{
  "success": true,
  "message": "连接所有设备成功"
}
```

失败：
```json
{
  "success": false,
  "message": "连接所有设备失败"
}
```

### 3.3 断开所有设备连接

**路径**：`/api/devices/disconnect-all`

**方法**：`POST`

**描述**：断开所有已连接设备的连接。

**请求体**：无

**响应**：

成功：
```json
{
  "success": true,
  "message": "断开所有设备连接成功"
}
```

失败：
```json
{
  "success": false,
  "message": "断开所有设备连接失败"
}
```

### 3.4 连接指定设备

**路径**：`/api/devices/connect`

**方法**：`POST`

**描述**：连接指定的设备。

**请求体**：

```json
{
  "deviceId": "设备ID"
}
```

**参数**：

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| deviceId | string | 是 | 要连接的设备ID |

**响应**：

成功：
```json
{
  "success": true,
  "message": "连接设备成功",
  "deviceId": "设备ID"
}
```

失败：
```json
{
  "success": false,
  "message": "连接设备失败",
  "deviceId": "设备ID"
}
```

参数错误：
```json
{
  "success": false,
  "message": "请求体中缺少deviceId",
  "deviceId": ""
}
```

### 3.5 断开指定设备连接

**路径**：`/api/devices/disconnect`

**方法**：`POST`

**描述**：断开指定设备的连接。

**请求体**：

```json
{
  "deviceId": "设备ID"
}
```

**参数**：

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| deviceId | string | 是 | 要断开连接的设备ID |

**响应**：

成功：
```json
{
  "success": true,
  "message": "断开设备连接成功",
  "deviceId": "设备ID"
}
```

失败：
```json
{
  "success": false,
  "message": "断开设备连接失败",
  "deviceId": "设备ID"
}
```

参数错误：
```json
{
  "success": false,
  "message": "请求体中缺少deviceId",
  "deviceId": ""
}
```

## 4. 设备类型

项目支持以下类型的设备：

| 设备类型 | 类型代码 | 描述 |
|---------|---------|------|
| 温湿度传感器 | WSD | 测量环境温度和湿度 |
| 气象传感器 | QX | 测量气象参数（如风速、风向、气压等） |
| 超大流量 | CDLL | 测量大气颗粒物浓度 |
| 碘采样器 | DCYQ | 采集空气中的碘同位素 |
| 碘化钠 | DHN | 测量放射性强度 |
| 干湿沉降 | GSCJ | 测量大气干湿沉降物 |

## 5. 示例请求

### 5.1 连接所有设备

```bash
curl -X POST http://localhost:8080/api/devices/connect-all
```

### 5.2 连接指定设备

```bash
curl -X POST http://localhost:8080/api/devices/connect \
  -H "Content-Type: application/json" \
  -d '{"deviceId": "D001"}'
```

### 5.3 断开指定设备连接

```bash
curl -X POST http://localhost:8080/api/devices/disconnect \
  -H "Content-Type: application/json" \
  -d '{"deviceId": "D001"}'
```

## 6. 安全考虑

### 6.1 认证

当前版本的API未实现认证机制，所有请求均可直接访问。在生产环境中，建议添加适当的认证措施，如API密钥或OAuth2.0。

### 6.2 速率限制

当前版本的API未实现速率限制，可能会受到DoS攻击的影响。在生产环境中，建议添加速率限制机制，限制单个IP的请求频率。

## 7. 故障排除

### 7.1 常见错误

| 错误消息 | 可能原因 | 解决方案 |
|---------|---------|---------|
| 请求体中缺少deviceId | 未提供设备ID | 在请求体中添加deviceId字段 |
| 连接设备失败 | 设备不存在或网络不可达 | 检查设备ID是否正确，确保设备网络连接正常 |
| 断开设备连接失败 | 设备不存在或未连接 | 检查设备ID是否正确，确保设备已连接 |

### 7.2 日志

服务器日志位于项目根目录的`app.log`文件中，包含所有API请求和错误信息，可用于故障排除。

## 8. 版本历史

| 版本 | 日期 | 变更描述 |
|------|------|---------|
| 1.0 | 2026-01-22 | 初始版本，实现基本设备管理API |

## 9. 联系方式

如有任何问题或建议，请联系项目维护人员。