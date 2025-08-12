
# 用户注册与登录 API 文档

## 1. 基本信息
- **基础 URL**: `http://106.55.54.216:25000`
- **数据格式**: 所有请求和响应均为 JSON
- **身份验证**:
  - 注册和登录不需要 token
  - 登录成功后返回的 `token` 用于后续验证

---

## 2. 接口列表

### 注册接口
- **URL**: `/register`
- **方法**: `POST`
- **请求参数**（JSON）:
```json
{
    "username": "string",   // 用户名
    "password": "string"    // 密码（明文）
}
```
- **返回示例**:
```json
{
    "message": "Registration successful! 注册成功",
    "status": 202,
    "token": "用户临时密钥",
    "uid": 1000001
}
```
- **状态码说明**:
  - 200：缺少必要参数
  - 201：用户名已存在
  - 202：注册成功

---

### 登录接口
- **URL**: `/login`
- **方法**: `POST`
- **请求参数**（JSON）:
```json
{
    "username": "string",  // 用户名
    "password": "string"   // 密码（明文）
}
```
- **返回示例**:
```json
{
    "message": "Login successful! 登录成功",
    "status": 102,
    "token": "用户临时密钥",
    "uid": 1000001
}
```
- **状态码说明**:
  - 100：缺少必要参数
  - 101：用户名或密码错误
  - 102：登录成功

---

### 管理员获取数据接口
- **URL**: `/admin_get_data`
- **方法**: `GET`
- **参数**（Query）:
```
token=管理员密钥
```
- **返回示例**:
```json
{
    "USER_DATABASE": [...],
    "TOKEN_DATABASE": {...},
    "message": "Admin page! 管理员页面",
    "status": 300
}
```
- **状态码说明**:
  - 300：获取成功
  - 301：无效 token

---

### 管理员更新数据接口
- **URL**: `/admin_send_data`
- **方法**: `POST`
- **参数**（Query）:
```
token=管理员密钥
```
- **请求 JSON**:
```json
{
    "USER_DATABASE": [...],
    "UIDMAX": 1000005
}
```
- **返回示例**:
```json
{
    "message": "Data received! 数据已接收",
    "status": 300
}
```

---
### 管理员获取Token接口
- **URL**: `/get_token`
- **方法**: `GET`   
- **参数**（Query）:
```
token=管理员密钥
```

- **返回示例**:
```json
{
    "message": "Token is valid! 有效的token",
    "status": 1000,
    "USER_DATABASE": "{...}"
 }
```
- **状态码说明**:
  - 1000：获取成功
  - 1001：无效 token

---
## 3.状态码说明
  - 100 登陆时缺少必要参数
  - 101 登陆时用户名或密码错误
  - 102 登陆成功
  - 200 注册时缺少必要参数
  - 201 用户名已存在
  - 202 注册成功
  - 300 管理员页面 获取用户数据库和token数据库 发送用户数据
  - 301 管理员页面 无效的token
  - 1000 游戏过程中数据正常获取
  - 1001 游戏过程中token失效
  - 1002 游戏过程中数据异常
---
## 4. 注意事项
1. 所有密码在传输前应通过 HTTP 进行传输。
2. token 仅在一定时间内有效。
3. 管理员接口应确保密钥安全，不要暴露给普通用户。
