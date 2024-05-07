# CheeseSoft

## 关于此项目

CheeseSoft，是主播[芝士饿晕了耶](https://space.bilibili.com/17992194/)的由粉丝群体自发组织开发的个人网页。项目整体使用HTML、CSS实现前端，使用Javascript实现后端和页面交互。项目原则上采用响应式布局以适配移动设备的正常显示。

### 项目结构

项目文件树如下：

```Text
CheeseSoft
    ├── /assets 
    │       ├── /picture
    │       └── /video
    ├── /css
    ├── /html
    │       └── /json
    ├── /javascript
    │
    ├   - index.html
    └   - README.md(this file)
```

其中：

+ `assets`：项目使用到的资源文件（包括视频、图像和xml等）
+ `css`：项目使用到的层叠样式表文件
+ `html`：项目中除了index.html外的页面文件
    + `json`：页面文件引用的json文件
+ `javascript`：项目使用到的js文件
+ `index.html`：主页面文件
+ `README.md`：此文件

*注：将/json放置在/html的原因是因为js的路径识别是基于引用的html文件确认的*

### 命名规范

项目整体采用小写字母+下划线的命名风格作为变量的命令规范，使用大写字母+下划线作为常量的命名规范

例如：

| 类型 | 错误示例                | 正确示例    |
| ---- | --------------------- | ----------- |
| 变量 | CheeseSoft（大驼峰）    | cheese_soft |
| 变量 | CHEeSEsOFT（大小写混用） | cheese_soft |
| 常量 | CHEeSEsOFT（大小写混用） | CHEESE_SOFT |

命名不可采用简写、缩写等形式，使用完整的单词更有利于构建自注释性（自文档化）代码。

针对资源文件的命名，项目不做要求

*注：变量常量的基本规范为：字符限定大小写字母下划线数字，数字字符不能成为第一个字符*

### HTML源代码规范

针对HTML源代码，使用如下规范：

+ [采用XHTML语法](#采用XHTML语法)
+ [使用四个空格缩进，严格缩进](#使用四个空格缩进，严格缩进)
+ [尽量使用语义化的标签](#尽量使用语义化的标签)
+ [尽量严格区分外部引用Javascript和内嵌Javascript](#尽量严格区分外部引用Javascript和内嵌Javascript)
+ [元素的id属性和class属性值视为变量，必须遵循变量命名规范](#元素的id属性和class属性值视为变量，必须遵循变量[命名规范](#命名规范))

#### 采用XHTML语法

HTML自身的语法是松散的，因此在标准HTML下，如下语法是正确的：

```HTML
<p>TEST TEXT
```

XHTML要求标签必须是两两成对或者封闭的的，因此上述代码在XHTML下是错误的，应当更改为如下语法：

```HTML
<p>TEST TEXT</p>
```

对于单标签，则：

```HTML
<img src="./assets/picture/test.png" />
```



XHTML标签必须正确的嵌套，如下嵌套在标准HTML下是正确的，但在XHTML规范中则为错误语法：

```HTML
<b><i>Contents</b></i>
```

正确的嵌套应当为：

```HTML
<b><i>Contents</i></b>
```



XHTML中，不论标签还是标签属性，都应当是小写，因此以下标签是错误的：

```HTML
<DIV CLASS="HASH">
    <P></P>
</DIV>
```



XHTML中，属性必须使用引号包裹，不论值是否为number，例如：

```HTML
<!--- 错误的属性值 --->
<div class=hash></div>

<!--- 正确的的属性值 --->
<div class="hash"></div>
```

此外，项目中优先使用半角双引号，而非单引号。

针对其它XHTML规范，请自行查询

#### 严格缩进

缩进是清晰展示对象结构的关键（即便HTML并不要求开发者如何缩进），项目采用四个空格作为缩进，而不是采用Tab缩进。一个良好的缩进应当是这样：

```HTML
<!DOCTYPE html>

<html>
    <head>
        <title>test</title>
        <meta chatset="UTF-8" />
    </head>
    
    <body>
        <p>TEST TEXT</p>
        <div>
            <p>TEST 2!</p>
        </div>
    </body>
    
    <footer>
        <span>Cheese Soft</span>
    </footer>
</html>
```

此外，合理化的使用空行分隔，也是保证代码可读性的关键要素。

#### 尽量使用语义化的标签

为了构建良好的自注释性代码，项目中尽量使用语义化的标签，不过由于总有部分内容需要使用到`<div>`这个标签，因此此规范为推荐性规范

#### 尽量严格区分外部引用Javascript和内嵌Javascript

HTML可以通过`<script>`标签内嵌或者引用外部的Javascript代码，两个操作都是由同一标签完成，因此区别内嵌和外部引用是有必要的，在一般情况下，下面的代码是不符规范的：

```HTML
<script scr="./javascript">
	console.log("Hello World");
</script>
```

符合规范的改写方法如下：

```HTML
<script scr="./javascript"></script>
<script>
    console.log("Hello World");
</script>
```

不过，在明确知道某个`<script>`块中会使用到某个外部js文件的情况下，混合写法便是符合规范的。例如

```HTML
<script src="./javascript/my_math.js">
    let pi = 3.14;
    my_tan(pi);
</script>
```

在这段代码中，我明确的使用了位于`"javascript/my_math.js`中的`my_tan()`函数，因此在这种情况下混合写法为符合规范的写法

#### 元素的id属性和class属性值视为变量，必须遵循变量[命名规范](#命名规范)

在HTML中为任意元素指定`id`或者`class`属性后，便可通过CSS指定元素`id`或者`class`修改这个元素样式，例如：

HTML：

```HTML
<div class="test">
    <div id="test1"></div>
</div>
```

CSS：

```CSS
.test {
    /* Style */
}

#test1 {
    /* Style */
}
```

因此，HTML中任意元素的`id`和`class`属性的值，也应当遵循变量[命名规范](#命名规范)

### Javascript规范

针对js源代码，使用如下规范：

+ [尽量使用`;`结束js代码](#尽量使用`;`结束js代码)
+ [必须使用`let`声明变量，必须在声明时初始化变量（即为定义）](#必须使用`let`声明变量，必须在声明时初始化变量（即为定义）)
+ [使用四个空格缩进，严格缩进](#使用四个空格缩进，严格缩进)
+ [函数遵循变量命名规范](#函数遵循变量[命名规范](#命名规范))
+ [字符串优先使用`"`包裹，其次才是`'`](#字符串优先使用`"`包裹，其次才是`'`)

#### 尽量使用`;`结束js代码

此为推荐性规范

#### 必须使用`let`声明变量，必须在声明时初始化变量（即为定义）

在js中，有两个关键字可以用于变量声明：

```javascript
var a1
let a2
```

为了更好的维护js代码，也为了让js在运行时更加符合直觉，项目中的js必须统一采用`let`关键字声明变量。

不过，上述代码即使剔除`var a1`，也是不符规范的，因为==变量并没有被初始化==。我们将变量在声明时就初始化一个值的行为，称为==定义==，此后也将使用这个词描述这种行为。

变量必须得到定义，就像这样：

```javascript
let a1 = 0
```

在声明时就给定一个值，能够防止潜在的问题，更好的让我们维护项目中的js。

#### 使用四个空格缩进，严格缩进

一个符合规范的标准的js缩进是这样的：

```javascript
function my_func() {
    let a = 0
    
    if (a === 1) {
        console.log(a + 1)
    }
    else {
        console.log("pass")
    }
}
```

上述代码中：

+ 使用了四个空格作为缩进，而非制表符
+ 非域指定的`{`没有单独成行

#### 函数遵循变量[命名规范](#命名规范)

此处不再赘述，举例：

```javascript
function my_func() {
    console.log("Hitman III")
}
```

#### 字符串优先使用`"`包裹，其次才是`'`

在js中，单引号`'`和双引号`"`都可以是字符串包裹符，就像这样：

```javascript
let string1 = 'Hello'
let string2 = "World"
```

为了符合直觉，项目中应当统一采用`"`作为字符串包裹符，因此上述代码应当改成这样：

```javascript
let string1 = "Hello"
let string2 = "World"
```

### CSS规范

针对CSS源代码，使用如下规范：

+ 颜色值统一采用十六进制颜色代码，例如：#66ccff



### 其它规范

此处对其它细节作出规范

#### JSON不能使用注释

在JSON中，不能使用任何注释