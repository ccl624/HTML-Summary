#### 1. 表单form
属性| 作用
--- | ----
action | 设置提交的地址或者路由
method | 提交的方式get、post

```
<form>
    <!-- input标签 -->
</form>
```
#### 2. HTML5新增的input标签类型
1. email，会提供基本的email地址验证功能
```
email:<input type="email"><br>
<input type="submit">
```
2. search，输入框会提供一个默认的清除搜索内容的按钮

```
search: <input type="search"><br>
<input type="submit">
```
3. url，会提供基本的url验证功能

```
url: <input type="url">
<input type="submit">
```
4. number，会提供一个number限制功能，可以设置范围，还有每次点击右边按钮跳跃的的数值

```
number: <input min="0" max="100" step="2" value="20" type="number">
<input type="submit">
```
```

```

5. tel，主要面向于手机，点击输入框会弹出手机的号码输入盘

```
tel: <input type="tel">
```
6. date，会提供一个日期控件，可以选择和操作日期

```
date: <input type="date"><br>
<input type="submit">
```
7. range，提供一个可调节范围的控件
    范围类型|作用
    --- | ---
    min | 设置最小值
    max | 设置最大值
    step|设置步长

```
range: <input type="range" min="0" max="100" step="10" value="0"><br>
<input type="submit" value="提交">
```
8. color，提供一个按钮点击可以选择颜色

```
color: <input id="color" type="color"><br>
```
示例：

```
//自定义调色板
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义调色器</title>
    <style>
        body {
            padding-left: 100px;
            padding-top: 100px;
        }
        .show {
            width: 300px;
            height: 300px;
            border: 1px solid rgb(0,0,0);
        }
    </style>
</head>
<body>
<div id="show" class="show"></div>
<br><br>
红:<input onchange="mychange()" id="red" min="0" max="255" step="1" value="255" type="range"><br>
绿:<input onchange="mychange()" id="green" min="0" max="255" step="1" value="255" type="range"><br>
蓝:<input onchange="mychange()" id="blue" min="0" max="255" step="1" value="255" type="range">
<script>
    function mychange(){
        var red = document.getElementById('red').value;
        var green = document.getElementById('green').value;
        var blue = document.getElementById('blue').value;

        var show = document.getElementById('show');

        show.style.backgroundColor = 'rgb('+red+','+green+','+blue+')';
    }
</script>
</body>
</html>
```
#### 3. 表单新元素
1. <datalist>，必须配合<input>标签使用，通过<input>标签的属性list关联<datalist>，<datalist>本身不显示

```
<input list="mylist">
<datalist id="mylist">
    <option>苹果</option>
    <option>小米</option>
    <option>锤子</option>
</datalist>
```
2. <progress>，提供一个进度条
```
<progress id="pro" max="100" value="0"></progress>
```
3. <meter>，计量表标签

```
<meter min="0" max="100" value="95" high="90" low="10"></meter>
```
#### 4. 表单新属性
1. autofocus
自动获取焦点，一般会设置在用户名输入框
2. placeholder
一般用来提示要输入的信息内容

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表单新属性</title>
</head>
<body>
<form id="myform" action="#">
    <input type="text" autofocus value="请输入你的用户名">
    <input type="text" placeholder="请输入你的用户名">
    <input type="submit">
</form>
<input type="text" form="myform">
</body>
</html>
```
#### 5. 表单验证属性 validity
##### 1. ValidityState：通过表单验证属性validity可以得到一个表单验证对象ValidityState，ValidityState对象提供一系列属性-代表了当前元素的状态

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>验证属性</title>
</head>
<body>
<form action="#">
    <input id="user" type="text" required><br>
</form>
<script>
    var user = document.getElementById('user');
    /*
        TODO 为所有的表单元素添加了一个表单验证属性 validity
        TODO * 通过 validity 属性得到一个表单验证对象 ValidityState
        TODO * ValidityState 对象提供一系列属性 - 代表了当前元素的状态
     */
    console.log(user.validity);
</script>
</body>
</html>
```
##### 2. ValidityState对象属性
1. valueMissing，value值为空字符串的时候valueMissing为true，反之为false
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="">
    用户名：<input id="user" type="text" required>
    <input type="submit">
</form>
</body>
<script type="text/javascript" >
    var user = document.getElementById("user");
    user.onblur=function () {
        console.log(user.validity.valueMissing);//value为空，输出为true
    };
    /*user.value="username";
    user.onblur=function () {
        console.log(user.validity.valueMissing);//value不为空，输出为false
    };*/
</script>
</html>
```
2. 其他的属性

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>有效状态</title>
</head>
<body>
<form action="#">
    <!-- TODO maxlength 属性 - 限制属性 -->
    用户名:<input type="text" id="user" required minlength="6" maxlength="8"><br>
    密码:<input type="text" id="pwd" pattern="[0-9]{6,8}"><br>
    email:<input type="email" id="mail"><br>
    年龄:<input type="number" id="age" min="18" max="50" step="2"><br>
    <input type="submit">
</form>
<script>
    var user = document.getElementById('user');
    /*
        TODO valueMissing - 对应元素的 value 属性值为空
        TODO * required 属性 - 验证表单元素不能为空
        TODO valueMissing配合 required 属性使用
     */
    user.onblur = function(){
        if(user.validity.valid){
            // TODO 表示输入正确
        }
        // TODO user.value == '' || user.value == undefined || user.value == null
        else if(user.validity.valueMissing){
            // TODO 为空
            console.log('用户名为空');
        }else if(user.validity.tooLong){
            // TODO 逻辑判断必须有的 -> 代码的健壮性
            console.log('你的用户太长了');
        }else if(user.validity.tooShort){
            console.log('你的用户太短了');
        }
    }
    var pwd = document.getElementById('pwd');
    pwd.onblur = function(){
        if(pwd.validity.patternMismatch){
            // TODO 正则表达式不匹配
            console.log('密码输入有误')
        }
    }
    var mail = document.getElementById('mail');
    mail.onblur = function(){
        // TODO typeMismatch 配合 email 或 url 类型使用
        if(mail.validity.typeMismatch){
            // TODO 类型不匹配
            console.log('电子邮件格式不对')
        }
    }
    var age = document.getElementById('age');
    age.onblur = function(){
        // TODO rangeUnderflow 匹配 min 属性
        if(age.validity.rangeUnderflow){
            // TODO 值小于 min
            console.log('年龄太小了')
        // TODO rangeOverflow 匹配 max 属性
        }else if(age.validity.rangeOverflow){
            console.log('年龄太大了')
        // TODO stepMismatch 匹配 step 属性
        }else if(age.validity.stepMismatch){
            console.log('年龄不匹配')
        }
    }
</script>
</body>
</html>
```



