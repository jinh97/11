#### 1、Redis五大基本类型的落地应用

命令不区分大小写、key区分大小写

hlep  @命令

- String
  - set k1 v2；get k1
  - mset k1 v1 k2 v2..........   mget k1 k2 k3
  - 应用场景
    - 统计点赞数，喜欢商品
    - 商品编号，订单编号生成。incr命令
- hash
  - 对应java-----Map<String,Map<k,v>>
  - 场景-------购物车

#### 2、还有哪些redis类型

- bitmap
- HyperLogLog
- GOE

