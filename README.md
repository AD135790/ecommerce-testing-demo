# 电商平台核心流程测试（Demo）

本项目模拟一个电商平台的核心业务流程：**注册 → 登录 → 下单**。  
测试目标：确保核心流程功能正确、接口规范、数据一致、性能可接受。  

---

## 一、测试流程
### 1. 需求分析
- 功能点：注册、登录、下单  
- 异常点：重复注册、错误密码、未授权下单、非法数量  

### 2. 测试计划
- **范围**：功能测试 + 接口验证 + 数据库校验 + 性能压测  
- **工具**：Postman / SQL / JMeter  
- **目标**：保证主流程稳定可用，异常场景能正确拦截  

---

## 二、测试用例（📂 test-cases/）
- `register.md`：注册用例（正常注册、空用户名、重复注册）  
- `login.md`：登录用例（正确登录、错误密码、空密码）  
- `order.md`：下单用例（正常下单、未授权、非法数量）  

👉 面试说法：  
“我根据需求写了黑盒测试用例，覆盖正常和异常场景。”

---

## 三、接口测试（📂 postman_collection/ + postman_environment/）
- `postman_collection.json`：包含注册、登录、下单三个接口  
- `ecommerce_env.json`（若你的项目中名为 `ecommercr_env.json`，同理）：环境变量（`base_url`、`token`）  
- 断言示例（登录后保存 token）：  
  ```javascript
  pm.test("状态码应为200", function () {
    pm.response.to.have.status(200);
  });
  pm.environment.set("token", pm.response.json().token);
# Extend the user's existing README with 

---

## 四、接口测试过程与操作（Postman）

### 接口列表
1) **注册接口**  
- Method: `POST`  
- URL: `{{base_url}}/api/register`  
- Body:
  ```json
  {
    "username": "test_user",
    "password": "123456",
    "email": "test@example.com"
  }
