## 编码原则
- 简明易懂，可读性强，方便他人修改维护。
- 编码规范，命名风格统一。
- 适当明确的代码注释。
- 避免《[项目中的不良编程习惯总结](https://facedrive.atlassian.net/wiki/spaces/FD/pages/44204247)》中提到的现象。

## 适用原则
- 所有新代码、新类、新需求开发采用本套编码规范
- 对于老代码上的小范围修改可以延续原有风格以保持局部的代码格式一致性，后续重构逐步演进。

## 规范用语与标签说明
- 【可以】：表示允许操作
- 【推荐】：最优的处理方式，但不是强制要求
- 【一般】：正常情况下按照规范执行，除非有特殊情况
- 【必须】：强制要求
- 【例外】：在满足特定条件时，允许操作。
- 如果没有上述标签，视为【一般】。

## 编码规范概要

### 基础格式
- 【必须】缩进用4个空格。如果喜欢用 tab，请在 IDE 中将 tab 的“宽度”设为4个空格。
- 【必须】全局函数采用小写加下划线的命名，如 `array_map()`
- 【必须】类名采用首字母大写，不加下划线，如 `VipController`
- 【必须】每个类单独一个文件
- 【必须】方法内代码块嵌套层级不超过 3 级；超过了要求重构逻辑或抽象方法
- 【推荐】代码行行宽：最好不超过 120 字符
- 【推荐】方法内代码块长度不超过两屏（80 行），最好不超过一屏（40 行）；超过了要求拆分方法

### 安全意识
- 【必须】不要以硬编码的形式将任何账号、密码写在代码中；而应该用系统环境变量或类似 `.env` 这种不被纳入 git 的文件来存储。
- 【必须】不要将敏感的用户信息输出到 log 文件中。常见的敏感信息有：
  - 信用卡卡号（如果必须写入 log，必须使用掩码遮盖）
  - 证件号码（如果必须写入 log，必须使用掩码遮盖）
  - 电话号码（如果必须写入 log，必须使用掩码遮盖）
  - 家庭住址
  - 姓名
  - 密码

## 代码检查
- 【推荐】在你的 IDE 上安装基本的代码检查插件
- 【推荐】PhpStorm 可以通过编辑区右侧滚动条的标识来确定代码干净程度
  - 黄色为有代码 warning，如命名空间未使用、变量使用时未定义、变量定义未使用等
  - 红色为代码有错误，如没有写结尾的 `;` 或 `{}` 未匹配成对等
  - 编辑区右侧滚动条最顶部显示绿色的勾，标识代码已整理干净

## 编码规范细节

### PHP文件
- 【必须】文件编码类型统一用 UTF-8 编码（不带 BOM）
- 【推荐】文件末尾留一个空行
- 【推荐】仅含 PHP 代码的文件最后的 `?>` 标签忽略
- 【必须】文件名
  - 类文件：`类名.php`
  - 配置文件：`全小写字母多单词用_分隔.php`

### 代码行
- 【必须】Unix 风格的换行: LF
- 【必须】适当添加空行来区分代码块增加代码可读性
- 【必须】每行不超过一条语句

### 关键词
- 【必须】PHP 关键词采用全小写。
  - 【例外】`AND`、`OR` 这 2 个和布尔运算有关的关键词应该大写。


### 命名原则
- 【必须】变量命名统一采用小写加下划线 `_` 分割，如 `order_id`。
- 【必须】方法命名统一采用驼峰格式，如 `camelFormat`；
- 【一般】方法命名时应以动词开头，如 `getOrderDetail()`
- 【必须】全局函数命名采用全小写字母加 `_` 格式，如 `array_map()`；全局函数只作为 PHP 函数库的补充，涉及业务的全局函数要求放到相关的类中。
- 【必须】类名采用单词首字母大写格式，如 `OrderController`；带类功能后缀，如 `-Controller`、`-Exception`、`-Operator`、`-Factory`、`-Storage`、`-Cache` 等
- 【推荐】命名中的单词一般不建议缩写和拼音。如果使用缩写，请使用公认、或团队内部约定俗成的缩写而不是自己杜撰。
- 【推荐】命名长度：不超过 40 个字符，最好不超过 25 个字符

### 代码注释

- 【必须】注释是代码的一部分，必须随着代码的更新而更新。
- 【必须】注释规范遵循 [PHP Doc 规范](https://docs.phpdoc.org/3.0/guide/references/phpdoc/tags/index.html#tag-reference)
- 【必须】所有核心关键方法、函数注释必须包含描述、参数说明、返回值说明。所谓“核心关键方法、函数”是指可能会被多次调用的方法或核心类中的方法。
- 【推荐】代码不明确的地方建议增加注释，存在复杂功能逻辑要求有明确的描述性注释
- 【可以】注释可以用中文

### 命名空间的使用
- 【必须】当存在时，use 命名空间必须在 namespace 定义之后空一行空行
- 【必须】当存在时，所有 use 命名空间必须在 namespace 定义之后
- 【必须】每行声明必须使用一个 `use` 关键词
- 【必须】use 代码块之后必须有一行空行

```php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...
```

### 类、属性、方法

> 这里的类指所有类、接口、trait。

- 【必须】首行为 `<?php`，后面不跟空格
- 【一般】`extends` 和 `implements` 关键字必须与类名字在一行
- 【推荐】`{` 放在类名声明末尾同一行，`}` 必须在代码块后面一行

```php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable {
    // constants, properties, methods
}
```

- 【推荐】`implements` 列表可以分拆成多行，每个一行；这么做时，第一项必须在下一行，并且之后每行只能有一个接口

```php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable {
    // constants, properties, methods
}
```

### 变量
- 【必须】消灭“魔法数字”，必须用变量或常量（或枚举值）代替并配合注释。
- 【推荐】避免无意义的临时变量。比如：
```php
<?php

$order_id = $order['id']; // 毫无意义，典型的废话
echo $order_id;

$order_id = $driver_list[0]['orders'][0]['id']; // 有意义，让代码更具可读性。
echo $order_id;
```

### 常量

- 【必须】所有常量必须使用全部大写，单词间使用 `_` 分隔

```php
<?php

namespace Vendor\Package;

class ClassName {
    const CONST_NAME = 'nothing';
}
```

### 属性

- 【必须】所有属性必须有可见性声明，即 `public`、`protected` 或 `private` 。
- 【必须】每个语句不能定义多余一个属性
- 【必须】private 属性名称使用前导 `_`。
- 【必须】除非必要，不要将属性定义为 `static` 。


```php
<?php

namespace Vendor\Package;

class ClassName {
    /* @var ClassName $foo */
    public $foo = null;
}
```

### 方法

- 【建议】方法名之后不能有空格。`{` 在 `)` 同一行，`}` 必须在代码块后面一行。`(` 后不能有空格，`)` 前不能有空格
- 【建议】尽量避免让一个方法与非必要的属性或方法产生交互。
- 【必须】如果一个方法不与任何属性或方法产生交互，必须将其定义为 `static` 。
- 【必须】可见性必须被声明在所有方法上，即 `public`、`protected` 或 `private` 。
- 【必须】方法内代码块嵌套层级不超过 4 级，最好不超过 3 级；超过了要求重构逻辑或抽象方法
- 【推荐】private 属性名称使用前导 `_`。
- 【推荐】方法内代码块长度不超过两屏（80 行），最好不超过一屏（40 行）；超过了要求拆分方法

```php
<?php

namespace Vendor\Package;

class ClassName {
    public function fooBarBaz($arg1, &$arg2, $arg3 = []) {
        // method body
    }
}
```

### 方法的参数

- 【一般】除非不可避免，否则不要以“传递引用（传址）”的方式传递参数。
- 【一般】避免非必要的默认值；带默认值的参数必须在参数列表的最后。
- 【一般】参数的数量建议不超过 5 个，最多不能超过 8 个参数；如超过了，要求重构函数或以数组、对象作为参数传递。
- 【必须】所有参数必须有类型提示，最好不要使用“mixed”作为类型提示。
- 【必须】在参数列表中，每个逗号前不能有空格，逗号后必须有一个空格。
- 【必须】参数列表可以被分成多行，每个子序列带一个缩进；当这么做时，列表的第一项必须在下一行，并且之后每行一个参数。
- 【必须】当参数列表被分成多行时，`)` 必须放置在 `{` 的一行，且中间有一个空格。

```php
<?php

namespace Vendor\Package;

class ClassName {
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

- 【必须】abstract, final 和 static：
  - 当存在时，abstract 和 final 声明必须在可见性声明之前
  - 当存在时，static 声明必须在可见性声明之后

```php
<?php

namespace Vendor\Package;

abstract class ClassName {
    protected static $foo;

    abstract protected function zim();

    final public static function bar() {
        // method body
    }
}
```
- 【必须】参数是数组时，用这种方式进行注释：
```php
<?php
/**
 * @param array $data = [ // 来自客户端的完整请求
 *     'order_id'    => 123,
 *     'grand_total' => 5.99,
 *     'tips'        => 1.99,
 * ]
 */
function foobar(array $data) {
    // do something
}
```

### 方法的返回值

- 【必须】必须标注返回值类型，不能出现 `mixed` 类型。
- 【必须】返回值类型和“冒号”之间必须有一个空格，如 `public function foobar(): string`。
- 【必须】不能出现啰嗦的 bool 返回值；比如：
```php
<?php
// 禁止
function foobar(int $a): bool
{
    if ($a > 0) {
        return true;
    } else {
        return false;
    }
}

// 应该
function foobar(int $a): bool
{
    return $a > 0;
}
```
- 【推荐】如果方法不能返回预期的类型，建议返回预期类型的“空值”；比如：
  * string 的空值：空字符串
  * array 的空值：空数组
  * object 的空值：null
  * int/float 的空值：0
  * Collection 的空值：一个空 Collection
- 【必须】如果返回值是数组，必须通过注释清晰的标注数组的结构。如果某个字段是可选的，也需要标出。
  - 【例外】如果 return 语句可以清晰的展现数组的结构，那么可以免去注释。

```php
<?php

/**
 *
 * @return array [
 *     'order_id' => 1111,
 *     'subtotal' => 5.99,
 *     'comment'  => '顾客备注', // 可选；如果顾客没有填写备注，该字段不会出现。
 * ]
 */
function foobar(): array
{
    return doSomething();
}

// 例外
function foobar(): array
{
    return [
        'order_id' => 1111,
        'subtotal' => 5.99 + $tips,
        'comment'  => '顾客备注',
    ];
}
```

### 方法与函数调用

方法与函数调用时：
- 【必须】方法或函数名与 `(` 之间不能有空格，`(` 之后不能有空格，`)` 之前不能有空格。
- 【必须】在参数列表中，每个逗号前不能有空格，逗号后必须有一个空格。
- 【必须】箭头 `->` 前后不能有空格。

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

- 【必须】参数列表可以被分成多行，每行带一个缩进；当这么做时，列表的第一项必须在 `(` 的下一行，并且之后每行一个参数。`)` 独占一行。

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

```php
<?php
// 参数换行原则：要么所有参数都在一行，参数要换行就每个参数单独放一行（包括第一个参数也需要单独一行）
// 可行的写法示例如下：

// 写法一：推荐这种，比较清晰
$query =  new AndQuery(
    new Query('type', \Verify\GuaranteedContract::TYPE),
    new Query('user', $user),
    new Query('status', EnumVerifyRequest::ACCEPT)
);
$vr = findOne('VerifyRequest', $query, ['size' => 20]);

// 写法二：喜欢行数少的同学可能会偏好这种
$vr = findOne('VerifyRequest', new AndQuery(
    new Query('type', \Verify\GuaranteedContract::TYPE),
    new Query('user', $user),
    new Query('status', EnumVerifyRequest::ACCEPT)
), ['size' => 20]);

// 写法三：这种也可以，但显得行数比较多，不太推荐
$vr = findOne(
    'VerifyRequest', 
    new AndQuery(
        new Query('type', \Verify\GuaranteedContract::TYPE),
        new Query('user', $user),
        new Query('status', EnumVerifyRequest::ACCEPT)
    ), 
    ['size' => 20]
);
```

- 【必须】函数或方法调用的 `)` 后不直接跟取键值操作

```php
<?php
/* 这种写法不推荐，原因为：
 * 1. 潜在报notice的可能；这个代码在确保函数返回数组且包含token键值时没问题，
 *    但对于一些分支逻辑下可能不会返回token值时，于是就会出notice
 * 2. 代码写起来没有那么清晰，特别是当函数调用或参数很长时
 */
$token = $this->getAccessTokenAndTtl($uid)['token'];

// 推荐以下替代两种写法，中间变量使得函数返回值结果的含义也会更清晰

// 写法一：增加临时变量，适合一次性调用的场景
$tokenTtl = $this->getAccessTokenAndTtl($uid);
$token = array_get($tokenTtl, 'token');

// 写法二：增加接口，适合多次调用的场景
public function getAccessToken($uid) {
    $tokenTtl = $this->getAccessTokenAndTtl($uid);
    return array_get($tokenTtl, 'token');
}
// 调用时访问新接口
$token = $this->getAccessToken($uid);
```

### 类的单例模式
- 【一般】除非必要，否则不要使用单例模式。参考《[我为什么不推荐使用单例模式？又有何替代方案？](https://blog.csdn.net/liyf2/article/details/108944916)》。绝大多数情况下，单例模式都可以被以下方案完美的替代：
  - 工厂模式
  - Laravel 提供的 IOC 容器
  - 程序员自己合理封装代码，保证不要在同一个生命周期内创建两个相同的对象

### 控制结构的代码基本规范

- 【推荐】控制关键字后必须有一个空格
- 【必须】`(` 后不能有空格，`)` 前不能有空格
- 【必须】`)` 和 `{` 之间必须有一个空格
- 【必须】结构体必须有一个缩进
- 【必须】`}` 必须在代码块下面一行
- 【必须】条件语句里不包含赋值语句

### if, elseif, else

- 【必须】`elseif` 代替 `else if`，使得看起来是一个关键字
- 【可以】对于 `if`...`return` 等只包含简单判断的流控制语句，并且书写者认为代码不换行可读性更高的时候，可以不加大括号和换行
- 其他格式如下

```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body
}

// 反例
if ($expr1) {
    // if body
} 
else {
    // else body
}
```

### swith, case

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

### while, do while
```
<?php
while ($expr) {
    // structure body
}

do {
    // structure body;
} while ($expr);
```

### for
```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

### foreach
```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

### try, catch
```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

### 闭包

- 【推荐】闭包的声明中在 `function` 关键词后应该有一个空格，在 `use` 关键词前后都应该有一个空格
- 【必须】`{` 必须与声明在一行，`}` 必须在代码块的下一行
- 【必须】其他空格逗号规则与函数定义相同
- 闭包的各种写法参考如下例子

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```
```php
<?php
$longArgsNoVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
    // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};

$longArgsLongVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};

$longArgsShortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
    // body
};

$shortArgsLongVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};
```
```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```
```php
<?php
$value = implode(
    ',',
    array_map(
        function ($v) {
            return $v instanceof Node ? $v->id : $v;
        },
        $uid
    )
);
$value = implode(',', array_map(function ($v) {
    return $v instanceof Node ? $v->id : $v;
},$uid));
```

### return 和 continue

- 【必须】如果 return 是代码块的最后一行，那么它的上方应该留有一个空行。比如：

```php
<?php
function foobar($a) {
    doSomething();
    
    return true;
}
```


- 【必须】如果 return/continue 不是代码块的最后一行，那么它的下方应该留下一个空行。 比如：

```php
<?php
// 推荐
function foobar($a) {
    if (!$a) return;
    
    doSomething();
}

foreach ($list as $item) {
    if (!$item) continue;
    
    $item = foobar($item);
}
```

### 函数使用

- 【必须】代码可读性考虑，禁用 `extract()`、`create_function()` 函数
- 【一般】使用 `strtotime()` 生成相对时间的时间戳，而不是类似 `$tow_days_ago = time() -> 3600 * 24 * 2` 这样的操作。

### 关于 Hack 代码
> 所谓“Hack 代码”，指为了应对 bug 的临时解决方案。

- 写完 Hack 代码后，必须在 Jira 上开设一个对应的任务分配给自己和相关同事，然后妥善处理相关代码。

### 错误处理
- 【一般】涉及业务逻辑、流程处理的部分，出错时应该抛出异常，而不是将错误状态码到处传递。
- 【可以】只要有恰当的理由，可以创建自定义异常；否则，尽量使用 PHP 提供的异常。

### 第三方类库
- 【必须】除非是 Laravel 框架本身提供的类库，任何第三方类库都应该先封装后再使用。这是因为：
  - 方便对该类库进行替换。如果没有封装，就会在项目中留下众多与该类库紧密相关的代码，难以清除。
  - 方便单元测试：有些第三方类库在进行测试时是有成本的，只有封装后才可能对其进行模拟。

## 代码可读性
- 【推荐】SOLID 原则
  - 《[图解你身边的 SOLID 原则]》(https://segmentfault.com/a/1190000022384751)
  - 《[超易懂！原来SOLID原则要这么理解！]》(https://www.cnblogs.com/chanshuyi/p/how-to-understand-solid-principle.html)
  - 《[设计模式之SOLID原则](https://learnku.com/docs/shxdledu/solid-principle-of-design-pattern/9281)》
- 【推荐】《[PHP 代码简洁之道（PHP Clean Code）](https://learnku.com/laravel/t/7774/the-conciseness-of-the-php-code-php-clean-code)》
- 【推荐】《[如何提高 model 操作代码的可读性](https://facedrive.atlassian.net/wiki/spaces/FD/pages/73334824/model)》
- 【推荐】《[提升正则可读性的六种方法](https://taoshu.in/regex-readability.html)》
- 【推荐】《[编写可读代码的艺术](https://book.douban.com/subject/10797189/)》

## 参考文献

- [PHP Standards Recommendations](http://www.php-fig.org/psr/)
- [百姓网 PHP 代码规范](https://github.com/baixing/Law/wiki/PHP-代码规范)
