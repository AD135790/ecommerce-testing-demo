# 🐛 BUG_REGISTER_001：注册接口未校验缺少密码

- **模块**：注册模块  
- **环境**：FakeStoreAPI (https://fakestoreapi.com)  
- **接口**：POST /users  
- **严重程度**：中等  

## 复现步骤
1. 打开 Postman  
2. 请求地址：`https://fakestoreapi.com/users`  
3. Method：POST  
4. Body → JSON 
输入：  
   ```json
   {
     "email": "john@example.com",
     "username": "johnd"
   }```

5.点击Send

## 实际结果
返回 201 Created

响应：
    ```json
   { "email":"sydney@fife", "id":"657", "createdAt":"2025-08-31T12:51:14.672Z" }
```


## 预期结果

应返回 400 Bad Request

响应：
    ```json
   {"error": "Missing password"
   }```

## 影响
产生不完整账号数据，后续登录/权限校验不可预期。
## 建议修复

后端对注册参数做必填校验：email、password 缺失时返回 400，并给出明确错误信息。