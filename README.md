# [iscroll](https://github.com/cubiq/iscroll)
### iscroll简介
#### 平滑滚动的网页
##### 主要的js
*    iscroll.js它是通用的脚本。它包括最常用的功能。
*    iscroll-lite.js这是一个精简版，它不支持滚动条，鼠标滚轮，按键绑定。但如果你需要的是滚动iscroll Lite是最小的，最快的解决方案
*    iscroll-probe.js,探索当前的滚动位置的一个分支，一般不用，这是作者特意建立的
*    iscroll-zoom.js, 增加缩放到标准的滚动
*    iscroll-infinite.js,可以做无限缓存滚动。处理很长的元素列表。iscroll无限使用的缓存机制，让你可以滚动一个潜在的无限数量的元素。

### iscroll的使用
#### 初始化
```
<script type="text/javascript">
var myScroll = new IScroll('#wrapper');
</script>
<div id="wrapper">
	<div id="scroller">
		<p  eiusmod tempor incididunt </p>
		<p  eiusmod tempor incididunt </p>
		<p  eiusmod tempor incididunt </p>
        <p  eiusmod tempor incididunt </p>
        <p  eiusmod tempor incididunt </p>
        <p  eiusmod tempor incididunt </p>
        <p  eiusmod tempor incididunt </p>
        <p  eiusmod tempor incididunt </p>
	</div>
</div>
```
* 尽量保持简单的DOM结构，iscroll必须应用在滚动区域的包装`#wrapper`标签中，它里面的就是要滚动的区域，但是只有wrapper的第一个孩子会滚动，就是`#scroller`,如果还有其他的孩纸是不会滚动的
* 添加位置`position:relative` or `absolute`到`#wrapper`上。只有这样，通常解决了大部分的问题。
#### 配置iscroll
```
var myScroll = new IScroll('#wrapper', {
    mouseWheel: true,//鼠标滚轮滚动
    scrollbars: true//滚动条
});
document.addEventListener('touchmove', function (e) { e.preventDefault(); }, false);//阻止默认事件
```
### 使用有错检查

####三个地方去检查一下

1. 确保#wrapper下只有一个#scroller元素，也就是说#scroller元素不能有兄弟元素。
1. 确保#scroller的高度设置正确。也就是说你想让内容在多大的一个框里面滑动要设置正确。这也是比较容易出错的地方。根据你的描述，我觉得你的	    这个高度可能和最里面内容的高度一样了。打开浏览器调试窗口去确认一下高度无误。
1. 在初始化iScroll之后，如果又在其里面的内容层加载了新的内容，一定要将你的iScroll实例刷新。尤其是在利用Angular写移动端的页面的时候，Aj    ax请求完数据之后，在回调函数里面写一句刷新你的iScroll实例的代码。

#### 理解内核
* `options.useTransform`,默认情况下，引擎使用CSS属性`transform`变换,但是性能损耗太大
* `options.useTransition`iscroll使用CSS`requestAnimationFrame`,在现代浏览器上的差异几乎不明显。在较旧的设备转换执行更好。
* `options.HWCompositing`,`translateZ(0)`此选项尝试通过添加translatez放在硬件层的滚动条（0）的变换CSS属性。这大大提高了性能，特别是在移动，但有情况下，你可能要禁用它（特别是如果你有太多的元素和硬件无法赶上）。

#### 基本的特征
* 参数名	      说明	可选值	默认值
* hScroll       是否允许水平滚动	false 否 true 是	true
* vScroll       是否允许垂直滚动	false 否 true 是	true
* bounce 	      是否超过实际位置反弹	false 否 true 是	true
* bounceLock    当内容少于滚动是否可以反弹	false 否 true 是	false
* momentum      是否开启拖动惯性	false 否 true 是	true
* lockDirection 当水平或垂直拖动时是否锁定另一边的拖动	false 否 true 是	true
* useTransform  是否使用CSS变形	false 否 true 是	true
* useTransition 是否使用CSS变换	false 否 true 是	false
* checkDOMChanges	是否自动检测内容变化	false 否 true 是	false
* topOffset	  已经滚动的基准值(一般用在拖动刷新)	数字值	0
* x	          滚动水平初始位置（负值）	数字值	0
* y	          滚动垂直初始位置（负值）	数字值	0

