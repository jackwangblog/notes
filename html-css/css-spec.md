﻿# CSS规范整理
对于一个有轻微强迫症的我来说，写CSS时命名真的很痛苦。有时候因为想不出好的命名要花掉好几分钟。严重影响工作效率。因此整理出一套CSS规范势在必行。（持续更新...）

## 使用什么选择器

* 不要使用ID，因为容易与javascript使用的ID混淆

* 少使用标签选择器
    * 影响了子孙的同名标签，不利于扩展
    * 重用性低
    * 更换标签很麻烦

* 少使用层级选择
    * CSS是从右至左渲染的，层级多了效率低。
    * 层级太深太多CSS文件也会变大
    * 重用性低
    * 无意提高了的优先级

具体怎么做还得看情况，比如：

```html
<div>
    <a href=""></a>
    <a href=""></a>
    ...
</div>
```
要给A标签加样式，A标签可能还有很多个，这种情况使用标签和层级会更合适点。因为如果使用class，势必会增加html文件的大小。

* 不要使用通配符(*)，属性选择器([attr])，多class(.a.b)。

* CSS3提供了很多高大上的复杂选择器，的确很方便，但是方便了开发者，却提高了解析器的计算复杂度。所以这类选择器是比较耗性能的。但是随着设备的升级，相比带来的好处，这点性能消耗似乎不足挂齿了。所以可以适当使用。

## 如何给class命名

* 如何避免冲突？
    * 对于全局公共的class，我们要靠人为约定去避免。
    * 对class进行分类，添加类别前缀。
    * 模块化编写CSS。将页面按模块划分。每个模块内部的class带上与该模块对应的前缀。

* 如何达到语义化？

    * 语义化的命名便于阅读与理解。但过于语义化了，类名必然会很长。而CSS要表达的东西是很直接的，没有很绕的逻辑。一个类定义了哪些样式是一目了然的。表现的怎么样也可以直接在浏览器里看出来。所以命名时可以精简些，使用缩写，不要一味的使用全拼。但也要注意，不能牛头不对马嘴。

* 连接符：
我喜欢使用"-"，看团队吧，统一就好。

* 命名：

    * 描述出元素是什么。有三点可以去衡量，一是内容，二是功能，三是表现。
    * 模块名尽量语义化，模块内的子类要加上对应的前缀。
    * 适当使用缩写，按音节截断。
    * 参考BEM，但不完全遵守。

```css
.demo-hd {} // header
.demo-bd {} // body
.demo-ft {} // footer
```

## 相关资料

* https://github.com/mdo/code-guide
* http://www.zhangxinxu.com/wordpress/2010/09/%E7%B2%BE%E7%AE%80%E9%AB%98%E6%95%88%E7%9A%84css%E5%91%BD%E5%90%8D%E5%87%86%E5%88%99%E6%96%B9%E6%B3%95
* http://www.orzpoint.com/profiling-css-and-optimization-note
* http://www.zhihu.com/question/21935157
* https://github.com/kejun/CSS-Code-Guideline
