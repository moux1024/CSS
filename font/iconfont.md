# iconfont使用总结
> 项目原架构为angularJS1.6.x+bootstrap3+LESS，使用fontawesome和部分自有图标库，使用angular指令实现自动混用，现需加入Ant Design风格图标，两套图标并用，Ant Design优先级高于原图标库

## iconfont基础知识
> 最初的iconfont借鉴了fontawesome的方式，利用伪元素content设置为Unicode码的方式，将图标作为字体引入HTML文档，后来添加了svg symbol方案支持多色图标。
> 详细的介绍大家看这里[Iconfont字体生成原理及使用技巧](http://www.iconfont.cn/help/article_detail?spm=a313x.7781069.1998910419.d6f75c492&article_id=1)
## css与font基础知识
> css定义了一些@标记语法，大家熟悉的有@import，@charset，@media等，@font-face是CSS3新增的属性，兼容性如下

| Feature	| Firefox (Gecko)	| Chrome	| Internet Explorer	| Opera	| Safari| 
| ------- |:-------------:| :---------:|:-------------:| :-----:|  :-----:|
| Basic support	| 3.5 (1.9.1)	| 4.0	| 4.0	| 10.0	| 3.1| 
| WOFF	| 3.5 (1.9.1)	| 6.0	| 9.0	| 11.10	| 5.1| 
| WOFF2	| 39 (39)[1]	| 38	| 未实现	| 24	| 未实现| 
| SVG Fonts[2]	| 未实现[3]	| (Yes)	| 未实现	| (Yes)	| (Yes)| 
| unicode-range	| 36 (36)| (Yes)	| 9.0	| (Yes)	| (Yes)| 

> 虽然表格看起来比较繁琐，不过iconfont已经做好了兼容代码，在这里我们只了解一下即可。[了解更多](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@font-face)
1. TureTpe Font(.ttf)格式：
.ttf字体是Windows和Mac的最常见的字体，是一种RAW格式，因此他不为网站优化；
2. OpenType Font(.otf)格式：
.otf字体被认为是一种原始的字体格式，其内置在TureType的基础上，所以也提供了更多的功能；
3. Web Open Font Format(.woff)格式：
.woff字体是Web字体中最佳格式，他是一个开放的TrueType/OpenType的压缩版本，同时也支持元数据包的分离；
4. Embedded Open Type(.eot)格式：
.eot字体是IE专用字体，可以从TrueType创建此格式字体；
5. SVG(.svg)格式：
.svg字体是基于SVG字体渲染的一种格式。

## 实施
### 方案
1. 在less里使用@font-face代码块，并下载woff、ttf文件到开发环境资源库，并不使用alicdn提供的链接。
2. 在Class声明中替换iconfont与fontawesome异名的图标名。
### 预期
> 未在新css中声明的font使用旧图标，新引入的font替换掉同名图标
### 结果
> 无法正常引入
> 无法正常覆盖
## 问题
> 原项目的打包路径复杂，独立的woff、ttf文件管理不方便，类似css中引入img时无法正常获取图片的问题。解决办法：直接在css中用base64引入字体文件，方便快捷
> 优先级问题。解决方法：直接!important标记走起，我们不会引入第三套icon了。
