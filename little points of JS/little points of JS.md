###01.关于数组
1. 数组：用一个变量存储一组值，用关键字Array来声明。
```JavaScipt
var beatles = Array(4);
```
2. 填充：向数组中添加元素，需要给出新元素的值和存放位置即元素的下标。
```JavaScipt
beatles[0] = "John";
```
3. 可以在声明数组时同时对它进行填充。
```JavaScipt
var beatles = Array( "John", "Paul", "George", "Ringo");
```
4. 数组元素可以是数值、字符串、布尔值、变量、另一个数组的元素以及其他数组。
```JavaScipt
var lennon = [ "John", "1940", false];
var names = [ "Ringo", "John", "George", "Paul"];
var beatles = [];
beatles[1] = names[3];
beatles[0] = lennon;
```
5. 关联数组：在填充元素时为每个新元素明确地给出下标，且下标不必局限于使用整数数字，可以用字符串。
```JavaScipt
var lennon = Array();
lennon["name"] = "John";
lennon["year"] = "1940";
lennon["living"] = false;
```
 本质上，在创建关联数组时，创建的是Array对象的属性。在JavaScript中，所有的变量实际上都是某种类型的对象。在上面的这个例子中，实际上是给lennon数组这个对象添加了name、year和living三个属性。

###02.关于对象
* 与数组类似，对象也是使用一个名字表示一组值。对象的每个值都是对象的一个属性。创建对象使用Object关键字，使用点号来获取属性。使用对象代替数组能提高脚本的可读性，使用语义化的字符串而不是整数作为下标访问元素。
```JavaScipt
var lennon = Object();
lennon.name = "John";
lennon.year = 1940;
lennon.living = false;
```
创建对象还可以使用花括号语法。
```JavaScipt
var lennon = { name:"John", year:1940, living:false};
```

###03.关于操作符

* 相等操作符==认为空字符串与false含义相同。
* 全等操作符===进行的是严格的比较，不仅会比较值，还会比较变量的类型。
* 严格不等于!==


###04.
* for循环最常见的用途之一是对某个数组里的全体元素进行遍历处理。
* array.length属性指的是在给定数组中元素的个数。
```JavaScipt
var beatles = Array( "John", "Paul", "George", "Ringo");
for( var count = 0; count < beatles.length; count++)
{
    alert(beatles[count]);
}
```

###05.对象类型

* 内建对象：JS提供的一系列预先定义好的对象。如数组Array对象、Date对象、Math对象。
* 宿主对象：由浏览器提供的预定义对象，包括Form、Image、Element等。


###06.节点类型

* 文档节点：document
* 元素节点：各种标签。
* 文本节点：文本内容，总是被包含在元素节点内部。
* 属性节点：用来对元素做出更具体的描述，class、id。


###07.给链接添加onclick事件处理函数

* 【案例】一个网页中有许多图片链接，需要在点击链接时，使图片出现在网页下方而不是转到另一个窗口。

 思路：通过增加一个“占位符”图片在主页上为图片预留一个浏览区域，在点击链接时把“占位符”图片替换为与那个链接相对应的图片。
```JavaScipt
function showPic(whichpic){
    var source = whichpic.getAttribute("href");
    var placeholder = document.getElementById("placeholder");
    placeholder.setAttribute("src",source);
}
```
 会遇到一个问题：点击链接时，不仅被调用的JavaScript代码会执行，链接被点击的默认行为也会被调用。
 
 解决：可以让JS代码执行完毕时返回一个值，这个值将被传递给那个事件处理函数。若返回值为true，onclick事件处理函数会认为“这个链接被点击了”；若返回值为false，onclick事件处理函数会认为“这个链接没有被点击”，就会调用showPic函数。
```JavaScipt
onclick="showPic(this);return false;"
```

###08.childNodes属性
 
* childNodes属性可以用来获取任何一个元素的所有子元素，是一个包含这个元素全部子元素的数组。需要注意的是，这个数组包含所有类型的节点。事实上，文档里几乎每一样东西都是一个节点，甚至空格和换行符。

```JavaScipt
function countBodyChildren(){
    var body_element = document.getElementsByTagName("body")[0];
    alert (body_element.childNodes.length);
}
window.onload = countBodyChildren;
```

###09.nodeType属性

* 元素节点的nodetype属性值是1，属性节点的nodetype属性值是2，文本节点的nodetype值是3。

###10.nodeValue属性

* 用来改变一个节点的值
* 需要注意的是，<p>、<h>等对象的值，并不是它们的文本内容。它们本身的nodeValue属性是一个空值。
```JavaScipt
var a = document.getElementById("a");
alert(a.nodeValue);
```
包含在其中的文本内容是另一个节点，是h1元素的第一个子节点。
```JavaScipt
alert(a.childNodes[0].nodeValue);
```

* nodeValue与value

 nodeValue是节点的值，value是元素节点的属性。


###11.JS平稳退化

* 网站的访问者可能未启用JS功能、不同浏览器对JS的支持程度不一样，会导致访问网站遇到各种各样的麻烦，此时需要对JS脚本进行优化完善，使网页虽然某些功能无法使用，但基本操作仍能顺利完成。

* 【案例】使用window对象的open()方法来创建新的窗口。window.open(url,name,features)
```HTML
<a href="#" onclick="popUp('http://www.baidu.com');return false;">EXAMPLE</a>
```
```JavaScipt
function popUp(winURL){
    window.open(winURL,"popup","width=480,height=320");
}
```
要使禁用JS功能的浏览器也能进入到新窗口，只需把href属性设置为真实存在的URL地址，让它成为一个有效的链接。
```HTML
<a href="http://www.baidu.com" onclick="popUp(this.href);return false;">EXAMPLE</a>
```

###12.JS向后兼容

* 对浏览器进行对象检测，检测浏览器对JS的支持程度.

 例：在使用getElementByTagName()方法之前先检查浏览器是否支持。如果浏览器不支持getElementByTagName的方法，就中途退出函数，确保浏览器不会因为代码出现问题，可以正常浏览。
```JavaScipt
window.onload = function(){
    if(!document.getElementsByTagName) return false;
    var lnks = document.getElementsByTagName("a");
    for(var i=0;i<lnks.length;i++){
        if(lnks[i].getAttribute("class")=="popup"){
            lnks[i].onclick=function(){
                popUp(this.getAttribute("href"));
                return false;
            }
        }
    }
}
```

###13.优化代码以保证应用流畅运行

1. 尽量少访问DOM。比如可以将要多次使用的对象存储在一个变量中，可以减少搜索DOM的次数。
2. 合并放置脚本。可以减少加载页面时发送的请求数量。
3. 压缩脚本。减少空格和注释，精简代码量。


###14.共享onload事件

* 常见
```JavaScipt
window.onload = function(){
    firstFunction();
    secondFunction();
}
```

* 当代码变得越来越复杂时，可以使用以下代码方便地使函数都在页面加载后执行。
```JavaScipt
function addLoadEvent(func){
    var oldonload = window.onload;
    //把现有的window.onload事件处理函数的值存入变量oldonload
    if(typeof window.onload != 'function'){
        window.onload = func;
    }//如果在这个处理函数上还没有绑定任何函数，就像平常那样把新函数添加给它
    else{
        window.onload = function(){
            oldonload();
            func();
        }
    }//如果已绑定函数，就把新函数追加到现有指令的末尾
}
```
 因此只需添加代码：
```JavaScipt
addLoadEvent(firstFunction);
addLoadEvent(secondFunction);
```

###15.appendChild方法

* 把新创建的节点插入某文档的节点树，让它成为该文档某个现有节点的一个子节点。
* 向节点添加最后一个子节点。
* 从一个元素向另一个元素中移动元素。
```JavaScipt
function myFunction(){
    var node=document.getElementById("myList2").lastChild;
    document.getElementById("myList1").appendChild(node);
}
```