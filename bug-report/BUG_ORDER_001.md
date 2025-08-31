# 🐛 BUG_ORDER_001：下单接口未校验数量和用户合法性

- **模块**：订单模块  
- **环境**：FakeStoreAPI (https://fakestoreapi.com)  
- **接口**：POST `/carts`  
- **严重程度**：高  

---

## 复现步骤
1. 打开 Postman  
2. 设置请求：`POST https://fakestoreapi.com/carts`  
3. Body → raw → JSON 输入：  
   ```json
   {
     "userId": 9999,
     "date": "2025-09-01",
     "products": [
       { "productId": 5, "quantity": 0 }
     ]
   }

4.点击Send

## 实际结果
返回 201 Created，订单依然创建成功。

响应内容：
```json
{
  "id": 12,
  "userId": 9999,
  "date": "2025-09-01",
  "products": [
    { "productId": 5, "quantity": 0 }
  ]

}
```


## 预期结果

应返回 HTTP 400 Bad RequestHTTP 400 Bad Request，返回“数量非法（quantity > 0）

## 影响

订单数量为 0 或负数仍可下单，影响库存和财务准确性。

非法用户依然能下单，存在安全与风控隐患。

## 建议修复

对 userId 做存在性校验，不存在的用户禁止下单。

对 quantity 做最小值约束（必须 > 0）。

返回清晰错误信息：400/404。