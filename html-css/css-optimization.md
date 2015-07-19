# CSS性能优化

### 浏览器工作原理
一外国开发者的研究成果： http://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/

上面这篇文章很值得一读，仔细阅读之后就会明白开发时为什么要做这些优化，或者你会自然而然的想到应该怎么去优化。我总结了几点需要记住的。

##### 1. 获取到文档内容后的工作流程
这是一个渐进的过程，并不是等整个HTML文档都下载完了才去进行的，在后面甚至会对前面已渲染过的元素重新渲染。
> * 解析HTML文档，构建DOM树
> * 同时解析CSS，构建呈现树
> * 布局
> * 绘制

##### 2. 同步网络模型
> 浏览器解析文档时如果遇到了`<script>`标记，会暂时停止解析文档(阻塞)，直到完成script的解析和执行。如果这个脚本是外部的，会先去下载。可以给`<script>`添加`defer`或`async`属性，告诉浏览器异步处理`<script>`。
> 遇到外部CSS文件时，也会先停止解析文档，先去下载CSS文件

##### 3. 样式计算
> 会为每个元素遍历整个规则列表来寻找匹配规则。
> 读取规则是从右至左

##### 4. 基于流的布局模型
> 大多数情况只需要遍历一次文档就能计算出元素的几何属性。但对表格布局时可能要计算多次。

##### 5. 定位方案
> * 普通
> * 浮动：元素先按照普通流进行布局，然后尽可能的向左或向右移动，直到遇到其他浮动元素或者遇到父元素的框。
> * 绝对：使用absolute、fixed来申明该定位方案，定义top、right、bottom、left来明确元素的位置。坐标参考最近的已定位的父级元素。

### 优化建议
1. 减少文档大小，加快文档下载。精简HTML结构，加快文档的解析。

2. `<script>`脚本最好放在文档最后，或异步加载，避免阻塞文档解析，减少白屏时间。

3. 减少样式规则，去掉多余的样式规则
> 存储样式规则是需要内存的，扫描规则也是需要时间的。所以规则越少越好。

4. CSS选择器越简单越好
> * 杜绝通配符`*`，尽量不要使用后代选择器和标签。不要使用表格布局
> * 不要画蛇添足，例如`div#s`,`div.s`
> * CSS3提供了很多很方便的选择器，但对解析引擎来说很复杂，所以尽量不要使用。

5. 减少`<img />`标签，并指定`<img />`的宽高

6. 不要使用CSS表达式

7. CSS文件放置head里面

8. 申明文档编码格式。
> 浏览器需要先确定编码格式再去渲染，这其中会有一些处理过程，还是直接申明避免这些吧。


### 重排和重绘优化
重排就是重新计算元素的位置，重新布局，然后会重新绘制。重绘会在元素外观改变时触发。重排一定会触发重绘，重绘就只是重绘啦。以下是常见触发重排的操作：
1. 元素的几何属性改变
2. 改变DOM树结构
3. 获取某些属性
> offsetTop、offsetLeft、offsetWidth、offsetHeight、scrollTop、scrollLeft、scrollWidth、scrollHeight、clientTop、clientLeft、clientWidth、clientHeight、getComputedStyle(currentStyle in IE)。

重排的代价是很高的，因为各种规则的计算相当复杂。一个元素发生了重排还有可能影响其他元素也发生重排。所以:
1. 减少不必要的重排操作
2. 缩小影响范围
3. 对于需要频繁操作几何属性的元素，让它脱离普通文档流，避免影响到其他元素。如JS动画。
4. 缓存获取到的属性值

### 最后的干货：Google开发者中心发表的性能优化建议
https://developers.google.com/web/fundamentals/performance/?hl=zh-cn

其他参考链接
http://developer.51cto.com/art/201311/417790.htm
http://developer.51cto.com/art/201311/418084.htm


