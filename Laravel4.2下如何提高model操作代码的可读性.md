## 创建 model 对象时

```php
<?php

// 可读性低
$order = new Order();
$order->cid = 111;
$order->subtotal = 10;
$order->save();

// 可读性高
$order = Order::create([
    'cid'      => 111,
    'subtotal' => 10,
]);
```
