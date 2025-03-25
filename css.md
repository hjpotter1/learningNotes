1.4 レスポンシブWebデザイン
メディアクエリ
link要素として指定する場合

スタイルシートに指定する場合

/*

@media以外の所は全てのサイズで読み込まれます。

*/

p {

color:red;

}

@media screen and (min-width:480px) {

/*　画面サイズが480pxからはここを読み込む　*/

p { color:#ededed;}

}

@media screen and (min-width:768px) and ( max-width:1024px) {

/*　画面サイズが768pxから1024pxまではここを読み込む　*/

p {}

}

@media screen and (min-width:1024px) {

/*　画面サイズが1024pxからはここを読み込む　*/

“读取style.css最多480px的屏幕尺寸”，style.css中描述的CSS应用于最多480px的屏幕尺寸。 如果值超过设置值（在这种情况下为宽度大小），则不会应用 CSS。

https://sole-color-blog.com/blog/71/

@media { ... }
@media all { ... }
@media (min-width: 500px) { ... }
@media all and (min-width: 500px) { ... }
@media (min-width: 500px) and (max-width: 800px) { ... }
端末の向きを判定する
//縦向きの場合
@media screen and (orientation:portrait){
  p {font-size: 1em; }  
}
//横向きの場合
@media screen and (orientation:landscape){
  p {font-size: 1.2em; }  
}
srcset属性
该元素可以根据浏览器的屏幕要求（宽度、高度、像素密度）加载不同的图像

<img src="img/example-img.jpg"
     srcset="img/example-img.jpg 1x,
             img/example-img@2x.jpg 2x"
     alt="Example image">
1x で解像度1倍のとき 2x で解像度2倍のとき ※Retinaのとき

imgタグを使った例

<img src="img/example-img.jpg"
     srcset="img/example-img-320.jpg 320w,
             img/example-img-640.jpg 640w"
     sizes="50vw"
>
320w, 640w ... w とは？

その画像を表示したい時のブラウザ幅px と捉えておけばOKです (昔はViewportのサイズだったらしいです)

sizes="50vw” の　vw とは

viewport widthの略称です ビューポートの幅に対する割合(%)　を指します

srcset="画像URL その画像を表示したい時の想定ブラウザ幅(px), ..."
と書いてしまえば良いです。

format-detection
スマートフォンでは例題のように数字列を電話番号と判断して関連するアプリにリンクする拡張があります。

<meta name="format-detection" content="telephone=no, email=no address=no" />
<a href="tel:030-0000-0000">030-0000-0000</a>
<a href="mailto:info@lpi.or.jp">info@lpi.or.jp</a><br>
<a href="http://maps.google.com/maps?q=東京都港区麻布台1-11-9">東京都港区麻布台1-11-9</a>
CSSスプライト
图标等小图片是通过HTTP为每个文件下载的，所以大量会影响页面的显示速度。 因此，将小图像排列在一张图像上，一次性下载它们，并通过指定 CSS 显示它们的技术称为 CSS 精灵。

在一张图像上放置多个图像，例如图标 通过 CSS 指定图像的坐标和大小来显示要使用的图像部分 由于图像加载一次完成，因此页面显示速度更快。

viewport
(E.) と記述することで、スマートフォンのデバイスの横幅で描画が行なわれるようになります。

移动设备上的viewport就是设备的屏幕上能用来显示我们的网页的那一块区域，viewport不局限于浏览器可视区域的大小，它可能比浏览器的可视区域要大，也可能比浏览器的可视区域要小。 一般来讲，移动设备上的viewport都是要大于浏览器可视区域的，这是因为考虑到移动设备的分辨率相对于桌面电脑来说都比较小，所以为了能在移动设备上正常显示那些传统的为桌面浏览器设计的网站，移动设备上的浏览器都会把自己默认的viewport设为980px或1024px（也可能是其它值，这个是由设备自己决定的），但带来的后果就是浏览器会出现横向滚动条，因为浏览器可视区域的宽度是比这个默认的viewport的宽度要小的。

https://qiita.com/ryounagaoka/items/045b2808a5ed43f96607

https://www.jianshu.com/p/cc81197b0886

利用meta标签对viewport进行控制
移动设备默认的viewport是layout viewport，也就是那个比屏幕要宽的viewport，但在进行移动设备网站的开发时，我们需要的是ideal viewport。那么怎么才能得到ideal viewport呢？这就该轮到meta标签出场了。

我们在开发移动设备的网站时，最常见的的一个动作就是把下面这个东西复制到我们的head标签中：

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
该meta标签的作用是让当前viewport的宽度等于设备的宽度，同时不允许用户手动缩放。也许允不允许用户缩放不同的网站有不同的要求，但让viewport的宽度等于设备的宽度，这个应该是大家都想要的效果，如果你不这样的设定的话，那就会使用那个比屏幕宽的默认viewport，也就是说会出现横向滚动条。

这个name为viewport的meta标签到底有哪些东西呢，又都有什么作用呢？

meta viewport 标签首先是由苹果公司在其safari浏览器中引入的，目的就是解决移动设备的viewport问题。后来安卓以及各大浏览器厂商也都纷纷效仿，引入对meta viewport的支持，事实也证明这个东西还是非常有用的。

在苹果的规范中，meta viewport 有6个属性(暂且把content中的那些东西称为一个个属性和值)，如下：

width	设置layout viewport 的宽度，为一个正整数，或字符串"width-device"
initial-scale	设置页面的初始缩放值，为一个数字，可以带小数
minimum-scale	允许用户的最小缩放值，为一个数字，可以带小数
maximum-scale	允许用户的最大缩放值，为一个数字，可以带小数
height	设置layout viewport 的高度，这个属性对我们并不重要，很少使用
user-scalable	是否允许用户进行缩放，值为"no"或"yes", no 代表不允许，yes代表允许
每个移动设备浏览器中都有一个理想的宽度，这个理想的宽度是指css中的宽度，跟设备的物理宽度没有关系，在css中，这个宽度就相当于100%的所代表的那个宽度。我们可以用meta标签把viewport的宽度设为那个理想的宽度，如果不知道这个设备的理想宽度是多少，那么用device-width这个特殊值就行了，同时initial-scale=1也有把viewport的宽度设为理想宽度的作用。所以，我们可以使用

<meta name="viewport" content="width=device-width, initial-scale=1">
来得到一个理想的viewport（也就是前面说的ideal viewport）。

实际上，这就是响应式布局的基础。

フルードグリッド
レスポンシブWebデザインは、1つのHTMLファイルで様々な表示デバイスに応じてWebページのレイアウトやデザインを最適化して表示する手法です。

レスポンシブWebデザインを実現するための技術の1つであるフルードグリッド(Fluid Grid)は、ブラウザの幅に応じてグリッド(格子、方眼)の大きさを伸縮させます。ページ全体をグリッドで区切りコンテンツを配置していくデザイン手法である「グリッドデザイン」と、画面の幅に応じてコンテンツの横幅が可変となる「フルードデザイン」を組み合わせたものです。

<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>フルードグリッドのサンプル</title>
	<style>
		body{
			width:100%;
			}
		#box1{
			width:50%;
			height:100px;
			background-color:#00ffff;
		}
		#box2{
			width:25.5%;
			height:100px;
			margin-top:20px;
			border-radius:50%;
			background-color:#ffc0cb;
		}
	</style>
</head>
<body>
		<div id="box1">ブラウザの幅に応じて伸縮します。</div>
		<div id="box2"></div>
</body>
</html>


标签页指示器
在一个标签页组件中，我们可能想要为活跃的标签添加一个向下的三角形指示器，就像这样：
htmlコピー<button class="bg-[#48a9ff] text-white rounded-lg py-3 px-4 relative">
  标签文本
  <div class="w-0 h-0 absolute -bottom-2 left-1/2 transform -translate-x-1/2 border-l-[10px] border-r-[10px] border-t-[10px] border-l-transparent border-r-transparent border-t-[#48a9ff]"></div>
</button>
这里的关键CSS属性包括：

absolute -bottom-2 left-1/2 transform -translate-x-1/2：这些定位属性将三角形放置在按钮底部中央
border-t-[#48a9ff]：确保三角形的颜色与按钮背景色相匹配

# Flex-wrap vs Grid 布局比较

## Flex-wrap

### 优点
- 更灵活的一维布局方案
- 容易实现自动换行和动态空间分配
- 适合处理不定数量的元素
- 对内容尺寸变化响应更自然
- 实现水平/垂直居中较简单

### 缺点
- 不擅长处理复杂的二维布局
- 在某些特定布局场景下需要更多的嵌套
- 行与行之间的对齐可能需要额外处理

### 常用属性
```css
.flex-container {
  display: flex;
  flex-wrap: wrap | nowrap | wrap-reverse;
  gap: <length>;
  justify-content: center | flex-start | flex-end | space-between | space-around;
  align-items: center | flex-start | flex-end | stretch;
}
```

### 适用场景
- 导航栏
- 标签列表
- 自适应卡片列表
- 需要自动换行的按钮组
- 一维方向的布局需求

## Grid

### 优点
- 强大的二维布局能力
- 更精确的网格控制
- 可以同时控制行和列
- 支持区域命名和模板
- 适合复杂的响应式布局

### 缺点
- 对动态内容的适应性较差
- 配置相对复杂
- 学习曲线较陡
- IE浏览器支持有限

### 常用属性
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-template-rows: auto;
  gap: <length>;
  grid-auto-flow: row | column;
}
```

### 适用场景
- 整页布局
- 图片画廊
- 数据表格
- 仪表盘
- 需要精确对齐的复杂布局

## 选择建议

1. 使用 Flex-wrap 当：
   - 布局主要是一维的（行或列）
   - 需要处理不确定数量的元素
   - 需要简单的自适应换行
   - 元素大小可能动态变化

2. 使用 Grid 当：
   - 需要二维布局控制
   - 布局结构相对固定
   - 需要精确的位置控制
   - 需要处理复杂的响应式布局

3. 混合使用：
   - 可以在 Grid 布局内部使用 Flex 处理单个网格项
   - 根据不同的布局需求选择合适的方案
   - 利用两者的优势创建更灵活的布局

在实际项目中，这两种布局方式经常会结合使用，以达到最佳的布局效果。比如在你的按钮布局案例中，选择 Flex-wrap 是因为它更适合处理自适应的一维按钮组布局。
						  
