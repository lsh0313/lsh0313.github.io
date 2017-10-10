# 温故而知新之DOM总结篇


DOM：Document Object Model 文档对象模型
DOM 定义了访问 HTML 和 XML 文档的标准：

“W3C 文档对象模型 （DOM） 是中立于平台和语言的接口，它允许程序和脚本动态地访问和更新文档的内容、结构和样式。”

W3C DOM 标准被分为 3 个不同的部分：
核心 DOM - 针对任何结构化文档的标准模型
XML DOM - 针对 XML 文档的标准模型
HTML DOM - 针对 HTML 文档的标准模型
HTML DOM 是：

HTML 的标准对象模型
HTML 的标准编程接口
W3C 标准
HTML DOM 定义了所有 HTML 元素的对象和属性，以及访问它们的方法。


换言之，HTML DOM 是关于如何获取、修改、添加或删除 HTML 元素的标准。

DOM树1

DOM树2

DOM 节点

根据 W3C 的 HTML DOM 标准，HTML 文档中的所有内容都是节点：

整个文档是一个文档节点 （9）
每个 HTML 元素是元素节点（1）
HTML 元素内的文本是文本节点（3）
每个 HTML 属性是属性节点（2）
注释是注释节点（8）


1.节点划分
  节点层级：父节点 子节点 兄弟节点 
  节点的类型：元素节点(1)  属性节点(2) 文本节点(3) 注释节点(8) document节点(9)

节点树

2.children和childNodes的异同
同：得到的是数组，都有length值，可以通过下标来获取
异：1)children 非标准属性 只获取第一层子节点并且是元素（标签）节点 标准浏览器下不会代码中的换行解析成空白节点
   2)childNodes 标准属性 子节点。会获取所有的子节点，包含文本节点和其他等节点。有兼容问题  标准浏览器下会把代码中的换行解析成空白节点

3.查看节点类型：nodeType 返回节点类型 
   元素节点的 nodeType值为1；
   属性节点的 nodeType值为2；
   文本节点的 nodeType值为3；
   注释节点的 nodeType值为8；
   document节点的nodeType值为9；
  查看节点名称 ： nodeName 返回节点属性
    元素节点 nodeName : 元素的本身
    属性节点 nodeName : 属性名本身
    文本节点 nodeName : #text
    注释节点 nodeName : #comment
    document nodeName : #document
  查看节点的值： nodeValue 返回节点的值
    元素节点的 nodeValue : null
    属性节点的 nodeValue : 属性值
    文本节点的 nodeValue : 文本内容
    注释节点的 nodeValue : 注释的内容
    document的 nodeValue : null
4.父节点 obj.parentNode 获取元素的父节点
         obj.offsetParent 获取元素的父节点
以上两个方法都是将父级元素整体打包
 
导航节点关系
使用三个节点属性：parentNode、firstChild 以及 lastChild ，在文档结构中进行导航。
DOM 根节点
这里有两个特殊的属性，可以访问全部文档：
document.documentElement - 全部文档
document.body - 文档的主体

      
5.子节点
firstChild : 获取元素的第一个子节点 在标准和ie9下会获取到空白文本节点。
firstElementChild : 标准下获取第一个子元素节点，ie6/7/8不支持。
lastChild : 获取元素最后一个子节点 在标准和ie9下会获取到空白文本节点。
lastElementChild : 标准下获取最后一个子元素节点，ie6/7/8不支持。
children 获取元素所有的子节点，不包括空白文本节点
childNodes 获取元素所有的子节点，包括空白文本节点

6.兄弟节点
nextSibling：下一个兄弟节点 在标准和ie9下会获取到空白文本节点。
nextElementSibling：标准下获取下一个兄弟元素节点，ie6/7/8不支持。
previousSibling：上一个兄弟节点 在标准和ie9下会获取到空白文本节点。
previousElementSibling：标准下获取上一个兄弟元素节点，ie6/7/8不支持。

7.节点操作（增删改查）
hasChildNodes(): 返回true和false 判断元素有没有子节点
createElement():  创建元素
creatTextNode():  创建文本节点
appendChild()：appendChild方法接受一个节点对象作为参数,可以创建新的节点,放在子集元素的最后, 如果是结构里面已经有的子节点， 该节点会被调换到子元素的最后 
insertBefore(obj1,obj2)：obj1为插入元素，插入在obj2之前
replaceChild(obj1,obj2): 被替换节点被移除 如果是结构中已经有的节点，则是把已经有的节点换到该位置,被替换节点还是被移除
removeChild() : 删除节点
cloneNode(true／false) : 克隆节点 true 会把元素里的内容也复制下来 false 只会复制元素本身 默认为false
编程接口
可通过 JavaScript （以及其他编程语言）对 HTML DOM 进行访问。
所有 HTML 元素被定义为对象，而编程接口则是对象方法和对象属性。
方法是您能够执行的动作（比如添加或修改元素）。
属性是您能够获取或设置的值（比如节点的名称或内容）。

8.获取属性节点
    <div id="box" class="div fafa" test="nihao"></div>
1)获取元素的第一种方法:.属性名。通过.属性名的方式只能添加标准属性，自定义属性是添加不上的 比如obj.id/obj.className(注意必须是className)
2)获取元素的第二种方法:元素[""] 同上只能获取标准属性  如：obj["id”]/ obj["className"]
3)获取元素的第三种方法:getAttribute("")比如div.getAttribute("test”）此方法是DOM提供的方法
4）obj.attributes方式可以获取元素的所有属性，拿到的是一个类数组，我们可以通过下标的形式拿到每一个属性

9.设置属性节点：setAttribute(“ ”,””) ；比如：obj.setAttribute("hello","world");
   移除属性节点 removeAttribute(”“) ; 比如：obj.removeAttribute("test");
10.Node类型图示：


延伸：：：

常用DOM 对象方法
getElementById()	返回带有指定 ID 的元素。
getElementsByTagName()	返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。
getElementsByClassName()	返回包含带有指定类名的所有元素的节点列表。
appendChild()	把新的子节点添加到指定节点。
removeChild()	删除子节点。
replaceChild()	替换子节点。
insertBefore()	在指定的子节点前面插入新的子节点。
createAttribute()	创建属性节点。
createElement()	创建元素节点。
createTextNode()	创建文本节点。
getAttribute()	返回指定的属性值。
setAttribute()	把指定属性设置或修改为指定的值。

样式
1.获取样式

          <div style="width: 500px;height: 500px;border: 1px solid red;"></div>

  1) obj.style     //.style方式只能获取到行间样式 比如：obj.style.width/obj.style.background
  2) obj.attributes[0]   // style = "width:500px;height:500px;border:1px solid red;"
  3)在标准浏览器下获取计算后的样式  getComputedStyle(元素,null)[“属性名”]  只有content
         比如:console.log(getComputedStyle(div,null).width); //500px  
                 console.log(getComputedStyle(div,null)["width"]);//500px
  4)在IE下 getCurrentStyle[“”] 
         比如：div.getCurrentStyle["width"];//在chrome浏览器中报错
2. 获取页面宽高 
    1) document.body.scrollTop仅仅局限于谷歌浏览器、safari下获取页面高度
    2) document.documentElement.scrollTop 针对html的节点获取页面高度 ，用于除谷歌以外的其他浏览器，在谷歌中获取到的高度为0；

    折中写法：document.documentElement.scrollTop + document.body.scrollTop;
3.获取页面可视窗口宽高
 1)document.documentElement.clientHeight //获取窗口可视区域高度 支持IE Safari opera
    document.documentElement.clientWidth//获取可视区域窗口宽度 支持IE Safari opera
 2)window.innerHeight window.innerWidth 支持除IE以外的所有浏览器
 折中写法：
   document.documentElement.clientHeight + window.innerHeight; 
   document.documentElement.clientWidth + window.innerWidth ;
