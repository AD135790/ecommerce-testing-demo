
## 📄 示例：BUG_LOGIN_001.md

# 🐛 BUG_LOGIN_001：登录接口未校验密码正确性

- **模块**：登录模块  
- **环境**：FakeStoreAPI (https://fakestoreapi.com)  
- **接口**：POST /auth/login  
- **严重程度**：高  

## 复现步骤
1. 打开 Postman  
2. 请求地址：`https://fakestoreapi.com/auth/login`  
3. Method：POST  
4. Body → JSON 输入：  
   ```json
   {
     "username": "mor_2314",
     "password": "wrongpassword"
   }

5.点击Send

## 实际结果
返回 200 OK，并生成 token。


## 预期结果

应返回 401 Unauthorized

响应：
    ```json
   { "error": "Invalid email or password"
    }```

## 影响
认证逻辑被绕过，系统对任意用户凭任意密码发放 token

## 建议修复

必须核验邮箱/密码的真实匹配；失败时返回 401，并限制暴力尝试次数。