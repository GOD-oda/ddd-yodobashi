# ddd-yodobashi

## 対象
https://www.yodobashi.com/ec/support/beginner/delivery/index.html

## 関係する単語
- VO(Value Object)：値オブジェクト
- Entity：エンティティ

## モデリング

|日本語名|英語名|種類|制約|
-|-|-|-
|注文ID|OrderId|VO|ULID|
|注文|Order|Entity \| 集約ルート||
|注文商品|OrderItem|Entity||
|注文商品ID|OrderItemId|VO|ULID|
|注文商品金額|Price|VO||
|配送先|Shipping|VO||


```mermaid
classDiagram

class 注文 {
    <<Entity|集約ルート>>
  
    -注文ID
    -注文商品
    -配送先
  
    +shippingPrice() int
    +totalPrice() int
}
注文 --> 注文ID
注文 "1" o--> "1..n" 注文商品
注文 --> 配送先

class 注文ID {
  <<VO>>
}

class 注文商品 {
    <<Entity>>
  
    -注文商品ID
    -注文商品金額
}
注文商品 --> 注文商品金額
注文商品 --> 注文商品ID

class 注文商品ID {
    <<VO>>
}


class 注文商品金額 {
    <<VO>>
}

class 配送先 {
    <<VO>>
}



```
