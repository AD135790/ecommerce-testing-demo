# 🛒 下单模块测试用例（order.md）

| 用例编号       | 标题           | 输入数据                                   | 前置条件    | 操作步骤              | 预期结果                     |
|----------------|----------------|--------------------------------------------|-------------|-----------------------|------------------------------|
| TC_ORDER_01    | 正常下单       | product_id=101, quantity=2                 | 已登录      | 调用 /api/order 接口  | 返回 200，提示“下单成功”     |
| TC_ORDER_02    | 未登录下单     | product_id=101, quantity=2                 | 未登录      | 调用 /api/order 接口  | 返回 401，提示“未授权”       |
| TC_ORDER_03    | 数量为 0       | product_id=101, quantity=0                 | 已登录      | 调用 /api/order 接口  | 返回 400，提示“数量非法”     |
| TC_ORDER_04    | 数量为负数     | product_id=101, quantity=-5                | 已登录      | 调用 /api/order 接口  | 返回 400，提示“数量非法”     |
| TC_ORDER_05    | 商品 ID 不存在 | product_id=99999, quantity=1               | 已登录      | 调用 /api/order 接口  | 返回 404，提示“商品不存在”   |
| TC_ORDER_06    | 缺少字段       | quantity=2                                 | 已登录      | 调用 /api/order 接口  | 返回 400，提示“字段缺失”     |
| TC_ORDER_07    | 字段类型错误   | product_id=101, quantity="two"             | 已登录      | 调用 /api/order 接口  | 返回 400，提示“类型错误”     |
