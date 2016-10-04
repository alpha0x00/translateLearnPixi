#说明
这是官方提供的学习Pixi的文档，我做了翻译，方便查阅和复习
翻译当中有不准确的，请多多指正。
[官方 github 地址](https://github.com/kittykatattack/learningPixi)

`翻译：吴佳`

学习 Pixi
=============
> 这个教程教你如何使用Pixi rendering engine(Pixi渲染引擎）一步一步制作游戏和互动媒体(最好要更新到Pixi v4.0版本以上)。如果你喜欢这个教程，你肯定也喜欢这本书，[这本书包含了 pixi 百分之80的内容!](http://www.springer.com/us/book/9781484210956)

### 目录:
1. [介绍](#introduction)
2. [配置、安装](#settingup)
  1. [github 上下载 js 文件](#installingpixithesimpleway)
  2. [使用 Git 安装 Pixi](#installingpixiwithgit)
  3. [使用 Node and Gulp 安装 Pixi](#installingpixiwithnodeandgulp)
3. [ 创建舞台和渲染器 ](#renderer)
4. [Pixi 精灵](#sprites)
5. [使用 loader 向 texture cache 中加载图片](#loading)
6. [精灵的显示](#displaying)
  1. [Pixi 对象别名](#usingaliases)
  2. [关于loading的一些事情](#almalt)
  3. [使用javascript image对象或者canvas创建一个精灵](#mafdjc)
  4. [使用别名加载文件](#antli)
  5. [监控加载时的进度](#monitoringloadprogress)
  6. [更多关于Pixi loader](#moreaboutpixisloader)
7. [精灵定位](#positioning)
8. [精灵的大小和缩放](#sizenscale)
9. [精灵旋转](#rotation)
10. [继承自一个图片集来制作精灵（来自雪碧图等）](#tileset)
11. [定义一个‘纹理’的集合（理解为使用定义好的 json 文件或者对象来制作）](#textureatlas)
12. [加载’纹理‘集合](#loadingatlas)
13. [使用一个定义了‘纹理’的集合创建精灵](#createsprites)
14. [移动精灵](#movingsprites)
15. [使用精灵的‘速度’属性](#velocity)
16. [Game states](#gamestates)
17. [键盘事件](#keyboard)
18. [精灵组](#grouping)
  1. [局部定位和全局定位](#localnglobal)
  2. [使用‘粒子容器’创建精灵组](#spritebatch)
19. [Pixi 的图元](#graphic)
  1. [长方形](#rectangle)
  2. [圆形](#circles)
  3. [Ellipses](#ellipses)
  4. [圆角矩形](#roundedrects)
  5. [线](#lines)
  6. [多边形](#polygons)
20. [文本显示](#text)
21. [碰撞测试](#collision)
  1. [The hitTestRectangle function](hittest)
22. [游戏案例: Treasure Hunter](#casestudy)
  1. [setup初始化游戏](#initialize)
    1. [创建游戏场景](#gamescene)
    2. [创建地牢、冒险家、入口（门)、宝藏](#makingdungon)
    3. [创建‘怪物’](#makingblob)
    4. [创建‘生命‘条](#healthbar)
    5. [创建提示消息](#message)
  2. [开始玩游戏](#playing)
  3. [冒险家进行探险](#movingexplorer)
    1. [移动事件(键盘)](#containingmovement)
  4. [怪物移动事件](#movingmonsters)
  5. [监听碰撞](#checkingcollisions)
  6. [如何赢得游戏](#reachingexit)
23. [关于更多‘精灵’的扩展](#spriteproperties)
24. [让 pixi 变得更好](#takingitfurther)</br>
  i.[Hexi](#hexi)</br>
25. [支持 Pixi 项目](#supportingthisproject)

<a id='introduction'></a>
介绍
------------
Pixi是一个非常快速的2D画面渲染引擎。 这意味着什么？这意味着它可以帮助你显示，动画和管理交互式图形，这样很容易为你做出使用JavaScript和HTML5等技术的游戏和应用程序。它有一个很爽的，整洁的API，包括许多功能，比如支持纹理地图和动画精灵（交互式图像）。它也可以带给你一个完整的场景图，让你可以创建嵌套精灵（精灵里面的精灵）的层次结构，以及让你直接连接鼠标和触摸事件精灵。而且，最重要的是，Pixi是很优秀的，你可以定义自己的风格，尽情的使用，并且可以和其他框架整合在一起使用。

Pixi的 API 是由Macromedia/Adobe Flash制作的，所以 Flash 的开发人员会觉得很舒服，其他动画渲染引擎使用的 API：CreateJs、Starling, Sparrow and Apple’s SpriteKit；Pixi 相对这些而言并不是一个游戏引擎，这没错，因为 Pixi 可以让你随心所欲的进行游戏和一些’游戏周边‘的开发。

本教程中，你会了解 Pixi 具备很强大的图像渲染功能和场景制作能力。而且可以使用质子如何使粒子效果，以及如何使用 Pixi 制作自己的游戏引擎，但是 Pixi 远远不止这些，Pixi 还可以创造更加出色的交互是媒体应用，并且应用的手机上。

开始教程之前你应该知道哪些东西？你需要适当了解Javascript和 Html Css3技术，只要你渴望学习并且积极向上，那么就开始本教程吧
在写代码之前，请使用文件夹创建一个工程，并且准备一个服务器部署工程，否则 pixi 无法正常运行。

<a id='settingup'></a>
配置、安装
----------
<a id='installingpixithesimpleway'></a>
### github 上下载 js 文件 

从[Pixi's GitHub
Repo](https://github.com/pixijs/pixi.js/tree/master/bin)上下载 `pixi.min.js` 最高版本.

创建一个Html文件，引入 `pixi.min.js` 并在控制台输出PIXI对象，`console.log(PIXI);`

```html
<!doctype html>
<meta charset="utf-8">
<title>Hello World</title>
<body>
<script src="pixi.min.js"></script>
<script>

//Test that Pixi is working
console.log(PIXI);

</script>
</body>
```
如果在控制台看出输出的PIXI对象信息，恭喜你，你可以尽情使用了

<a id='installingpixiwithgit'></a>
### 使用 Git 安装 Pixi

你也可以[从这里获取 git 版的 Pixi](https://github.com/kittykatattack/learningGit)
获取到pixi.js后就可以使用了

<a id='installingpixiwithnodeandgulp'></a>
### 使用 Node and Gulp 安装 Pixi

[详情请查看 Pixi 的 Github，上面有安装步骤](https://github.com/GoodBoyDigital/pixi.js)

<a id='renderer'></a>
创建舞台和渲染器
-------------------------------
第一步，创建一个矩形区域来显示图形，可以使用 Pixi 的 `renderer` 对象来创建，可以生成一个 `canvas`类型的 html 元素显示图形信息，接着，你要创建一个特殊的 Pixi `Container` 容器，我们称之为舞台 `stage`，舞台就是我们的根元素,所有的显示元素都依赖根元素进行显示。
在 html 页面的 `<script>` 标签中写入：

```js
//Create the renderer
var renderer = PIXI.autoDetectRenderer(256, 256);

//Add the canvas to the HTML document
document.body.appendChild(renderer.view);

//Create a container object called the `stage`
var stage = new PIXI.Container();

//Tell the `renderer` to `render` the `stage`
renderer.render(stage);
```

这段代码意味着你已经开始使用 Pixi ，创建了一个长、宽为256px 的元素，Pixi 转换为 Dom元素渲染出来。

Pixi 的 `autoDetectRenderer` 方法可以自动计算使用Canvas绘图API或WebGL渲染图形。第一个参数为：宽度，第二个参数为高度，第三个参数可选，是为对象，可以设置反锯齿、透明度和分辨率信息。

```js
renderer = PIXI.autoDetectRenderer(
  256, 256,
  {antialias: false, transparent: false, resolution: 1}
);
```
第三个参数的具体使用 
[请查阅文档](http://pixijs.github.io/docs/PIXI.CanvasRenderer.html)
和
[WebGLRenderer文档](http://pixijs.github.io/docs/PIXI.WebGLRenderer.html)

这些选项都是做什么的呢？

```js
{antialias: false, transparent: false, resolution: 1}
```

`antialias` 用来平滑字体、图元的边缘 (WebGL抗锯齿跨平台性能不太好，如果要使用，需要测试真实效果)
`transparent` 设置画布的背景透明度
`resolution`  兼容更多的屏幕分辨率（resolution 设置为1可以适配大多数的分辨率）
本教程这个参数设计的比较少；[更多查阅](http://www.goodboydigital.com/pixi-js-v2-fastest-2d-webgl-renderer/)


(注意: 如果使用 WebGl的`dataToURL`方法，可以将renderer的 `preserveDrawingBuffer`参数设置为 `true`)

Pixi 的渲染器默认使用WebGL(`autoDetectRenderer`),因为WebGL速度很快，如果要强制指定 canvas 或者 强制指定 webGL
可以使用以下两个方法

```js
//只需要设置宽高
renderer = new PIXI.CanvasRenderer(256, 256);
renderer = new PIXI.WebGLRenderer(256, 256);
```

`renderer.view` 是一个 `Canvas`对象，可以对`renderer.view`进行样式修饰

```js
renderer.view.style.border = "1px dashed black";
renderer.backgroundColor = 0x061639;//16进制
renderer.view.width=‘’；
renderer.view.height=‘’；
renderer.resize(width,height);//resize方法可以重置canvas 的大小
//也可以将 canvas 填充整个屏幕
renderer.view.style.position = "absolute";
renderer.view.style.display = "block";
renderer.autoResize = true;
renderer.resize(window.innerWidth, window.innerHeight);
```

(重要提示: `stage` 的 `width` 和 `height` 属性代表了舞台的大小，并不是画布的大小)


如何将你的画布按照比例缩放（适配）到任何浏览器窗口？[点击这里查阅](https://github.com/kittykatattack/scaleToWindow).

<a id='sprites'></a>
Pixi 精灵
------------

上一章节中，我们创建了一个stage（舞台）对象

```js
var stage = new PIXI.Container();
```

`stage` 是 Pixi 的 `Container` 对象. 你可以将 `stage`想象为一个盒子，你可以在盒子里面装任何你想装的东西。
`stage` 将作为你屏幕上的根容器节点，因为 Pixi 需要这么一个容器来呈现内容：

```js
//目前，我们的stage是空空如也的...
renderer.render(stage);
```

(注意: 你可以定义你想定义的根容器名字：例如`scene` 或者 `root` .本教程中，我们约定`stage`为我们的根容器)


因此，接下来我们要放一些什么样的元素在舞台上呢？我们所说的`sprites`精灵是舞台的元素，其实就是特殊的图像。你可以使用代码控制他们的位置、大小、交互方式等等，精灵对于Pixi 是非常重要的，如果你理解了精灵如何在舞台上展现，那么你将会很快学会 Pixi.

Pixi 有一个叫做`Sprite` 的类，这个类负责生产、创建精灵，有三种方法创建精灵：

- 从一个单一的图形文件
- 作为子图像继承自一个大图（雪碧图、或者为一个游戏专门制作的图形组文件等）
- 来自一个定义了`texture atlas`的 JSON 文件，包含了图形的位置、大小信息等

在学习这三种方法之前，我们可以先从简单的显示作起。

<a id='loading'></a>
使用 loader 向 texture cache 中加载图片
-------------------------------------

因为Pixi渲染引擎使用 WebGL 渲染时， 需要处理成GPU 可以识别的格式，我们把这种格式叫做`texture`,如果你需要显示一个图形，那么你需要把图形转换为`texture`,来保证快速渲染，Pixi 使用`texture cache`来存储、引用所有的 `texture`

```js
//创建一个 texture 纹理
PIXI.utils.TextureCache["images/cat.png"];
var texture = PIXI.utils.TextureCache["images/anySpriteImage.png"];
//使用 texture 创建一个 sprite 精灵
var sprite = new PIXI.Sprite(texture);
```
图片在网络传输到显示出来，有一个过程，如何将加载和转换为`texture`合在一起呢？你可以使用Pixi的`loader`对象；Pixi 的`loader`对象很强大，她可以加载各种类型的图像，你可以在图像加载完成后，调用指定的 setup 函数来完成之后的显示。

```js
PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  //This code will run when the loader has finished loading the image
}
```
[Pixi 的开发团队对loader的使用建议](http://www.html5gamedevs.com/topic/16019-preload-all-textures/?p=90907)

如果你使用了Pixi的 loader 加载图像，在创建 sprite 精灵时，需要从loader.resources中获取texture

```js
var sprite = new PIXI.Sprite(
  PIXI.loader.resources["images/anyImage.png"].texture
);
```
下面列举了常用的 loader 语法格式：

```js
//加载图形数组
loader.add(
	[
	'src/img/girl.jpg',
	'src/img/girl2.jpg'
	]
).load(setup);
//g1、g2为别名, progress为进度属性，可监听加载进度，loadProgressHandler为回调
loader.add("g1","src/img/girl.jpg")
            .add("g2","src/img/girl2.jpg")
            .on("progress", loadProgressHandler).load(setup);

            
function setup(){
	//属性获取
	loader.resources['src/img/girl.jpg'];
	//从loader中获取texture
	loader.resources.g1.texture;
	loader.resources.g2.texture;
	
	//创建texture
	var texture = PIXI.loader.resources["src/img/girl.jpg"].texture;
	var texture2 = PIXI.loader.resources.g2.texture;
	
	//创建精灵
	var sprite = new PIXI.Sprite(texture);
}
function loadProgressHandler(loader,resource){
	console.log(loader);
	console.log(resource);
}
```

<a id='displaying'></a>
精灵的显示
------------------

上一步，我们用 loader 加载图形转换为 texture，并且创建了 sprite 精灵，接下来，我们要讲 sprite 显示出来；如果不渲染舞台的话，我们创建的精灵是不能自动显示的。

```js
//将精灵加入舞台
stage.addChild(sprite);
//渲染舞台到画布
renderer.render(stage);
```

在我们继续之前  `examples/images` 文件夹中有加载一个图片的示例，可以打开查看哦。
我们可以写一个完整显示图片的代码

```js
var stage = new PIXI.Container(),
    renderer = PIXI.autoDetectRenderer(256, 256);
document.body.appendChild(renderer.view);

PIXI.loader
  .add("images/cat.png")
  .load(setup);

function setup() {
  var cat = new PIXI.Sprite(
    PIXI.loader.resources["images/cat.png"].texture
  );
  stage.addChild(cat);
  renderer.render(stage);
  
  //从舞台上如何删除一个精灵？
  stage.removeChild(anySprite);
  anySprite.visible = false;//官方建议
}
```

<a id='usingaliases'></a>
### Pixi 对象别名

说白了，就是为Pixi的对象创建一个简短的名称，便于使用，请注意变量作用域；

```js
//Aliases
var Container = PIXI.Container,
            autoDetectRenderer = PIXI.autoDetectRenderer,
            loader = PIXI.loader,
            resources = PIXI.loader.resources,
            Sprite = PIXI.Sprite,
            pixiUtil = PIXI.utils;

var stage = new Container(),
    renderer = autoDetectRenderer(256, 256);
document.body.appendChild(renderer.view);

loader
  .add("images/cat.png")
  .load(setup);
function setup() {
  var cat = new Sprite(resources["images/cat.png"].texture);  
  stage.addChild(cat);
  renderer.render(stage);
}
```


<a id='almalt'></a>
###关于loading的一些事情

上面我们了解了一些 loading 的用法，我们建议使用标准的模板（比如 json格式的数据）来加载显示精灵，接下来我们介绍一些 loading 的基础功能。这是必须要了解的。

<a id='mafdjc'></a>
####使用javascript image对象或者canvas创建一个精灵

除了loader，你可以可以使用BaseTexture来创建texture和sprite; BaseTexture的好处是可以从Canvas中获取。

```js
var base = new PIXI.BaseTexture(anyImageObject),
    texture = new PIXI.Texture(base),
    sprite = new PIXI.Sprite(texture);
    
//from canvas
var baseCanvas = new PIXI.BaseTexture.fromCanvas(anyCanvasElement),
```

你可以可以制定一个sprite精灵的texture纹理为任何一张图形，在你的游戏或者应用中可以随时更改。

```js
anySprite.texture = PIXI.utils.TextureCache["anyTexture.png"];
```

<a id='antli'></a>
####使用别名加载文件

Pixi的loader加载图形时，可以使用一个图形数组，也可以指定别名来加载

```js
//loader an array
PIXI.loader
  .add(["images/cat.png","images/dog.png"])
  .load(setup);
// catImage is Alias
PIXI.loader
  .add("catImage", "images/cat.png")
  .load(setup);
```
使用别名后，创建 sprite 时候也可以方便获取

```js
var cat = new PIXI.Sprite(PIXI.loader.resources.catImage.texture);
```

<a id='monitoringloadprogress'></a>
####监控加载时的进度

可以使用progress来做一些 loading 等待效果，使用详见代码：

```js
PIXI.loader
  .add([
    "images/one.png",
    "images/two.png",
    "images/three.png"
  ])
  .on("progress", loadProgressHandler)
  .load(setup);

function loadProgressHandler(loader, resource) {

  //Display the file `url` currently being loaded
  console.log("loading: " + resource.url); 

  //Display the precentage of files currently loaded
  console.log("progress: " + loader.progress + "%"); 

  //If you gave your files names as the first argument 
  //of the `add` method, you can access them like this
  //console.log("loading: " + resource.name);
}

function setup() {
  console.log("All files loaded");
}
```

(注意: 可以通过`resource.error`和`resource.data`来查看处理加载时候的错误信息)

<a id='moreaboutpixisloader'></a>
####更多关于Pixi loader

Pixi 的 loader 使用方法：add()多次使用

```js
.add('key', 'http://...', function () {})
.add('http://...', function () {})
.add('http://...')
```
加载时混合别名使用

```js
.add({
  name: 'key2',
  url: 'http://...'
}, function () {})

.add({
  url: 'http://...'
}, function () {})

.add({
  name: 'key3',
  url: 'http://...'
  onComplete: function () {}
})

.add({
  url: 'https://...',
  onComplete: function () {},
  crossOrigin: true
})
```
加载对象别名使用
```js
.add([
  {name: 'key4', url: 'http://...', onComplete: function () {} },
  {url: 'http://...', onComplete: function () {} },
  'http://...'
]);
```
(注意: 可以使用 `PIXI.loader.reset();`方法来将loader清空，加载新图形)

Pixi 的 loader 有很多高级功能，还可以加载更多的二进制文件；[在 github 上查看更多 loader 项目](https://github.com/englercj/resource-loader).

<a id='positioning'></a>
精灵定位
-------------------

显示你知道了如何创建精灵并显示，现在让我们来设置他们的位置和大小吧；直接看代码：

```js
var cat = new Sprite(texture);
cat.x = 96;
cat.y = 96;
//在加载完毕后再设置位置
function setup() {
  var cat = new Sprite(resources["images/cat.png"].texture);

  //Change the sprite's position
  cat.x = 96;
  cat.y = 96;
  
  //直接使用sprite.position方法设置
  sprite.position.set(x, y);

  stage.addChild(cat);
  renderer.render(stage);
}
```

<a id='sizenscale'></a>
精灵的大小和缩放
--------------

大小

```js
var cat = new Sprite(texture);
cat.width = 80;
cat.height = 120;
//在加载完毕后再设置
function setup() {

  //Create the `cat` sprite
  var cat = new Sprite(resources["images/cat.png"].texture);

  //Change the sprite's position
  cat.x = 96;
  cat.y = 96;

  //Change the sprite's size
  cat.width = 80;
  cat.height = 120;

  //Add the cat to the stage so you can see it
  stage.addChild(cat);
}
```

缩放

```js
//0.5为一半大小，2为一倍大小
cat.scale.x = 0.5;
cat.scale.y = 0.5;
cat.scale.x = 2;
cat.scale.y = 2;
//使用方法设置
cat.scale.set(0.5, 0.5);
```

<a id='rotation'></a>
精灵旋转
--------

可以通过设置`ratation`参数来让一个精灵旋转，[参考radians值来确定ratation](http://www.mathsisfun.com/geometry/radians.html)
```js
cat.rotation = 0.5;
```
旋转的时候都发生了什么？一个精灵的左上角的位置是使用`x` 和 `y`来确定的，这个点就叫做**anchor point（锚点、支点）**，rotation 属性就是围绕`锚点`进行旋转。默认是顺时针旋转。如果想让精灵以其他位置点旋转，需要更改精灵的`anchor`点属性：

```js
cat.anchor.x = 0.5;
cat.anchor.y = 0.5;
```
`anchor.x`和`anchor.y`代表精灵尺寸的长宽百分比，范围0~1.也可以使用方法设置：

```js
sprite.anchor.set(x, y)
```
设置精灵的`旋转锚点`也可以设置`pivot`来实现，`pivot`设置的是长宽的具体像素值：

```js
cat.pivot.set(32, 32)
```
如果你改变了旋转支点的位置，那么意味着x，y 原点位置也会改变。`anchor` 和 `pivot`的区别在于，一个按照百分比计算，一个按照具体像素计算位置。可以选择你喜欢的方式。

<a id='tileset'></a>
继承自一个图片集来制作精灵（来自雪碧图等）
--------------------------------------

我们学会了如何从单一图像穿件一个精灵，但是，作为一个游戏设计师，我们通常会使用**tilesets** (也称作**spritesheets**.)
瓦片集，一个 tileset 是一个单一的图像文件，包含我们最终使用的每个‘子图像’，例如，一个图像可以包含游戏人物和游戏背景。整个瓦片集 tileset 宽高为192px，每个子图像的大小为32*32大小，可以通过访问 tileset 来显示、缓存等。pixi 对此做了优化。你可以定义一个大小为矩形的区域，来提取子图像并且显示。
首先先加载`tileset.png`

```js
loader
  .add("images/tileset.png")
  .load(setup);
```
当瓦片集图像加载完后，我们来提取一个子图像显示：

```js
function setup() {

  //Create the `tileset` sprite from the texture
  var texture = TextureCache["images/tileset.png"];

  //Create a rectangle object that defines the position and
  //size of the sub-image you want to extract from the texture
  var rectangle = new Rectangle(192, 128, 64, 64);

  //Tell the texture to use that rectangular section
  texture.frame = rectangle;

  //Create the sprite from the texture
  var rocket = new Sprite(texture);

  //Position the rocket sprite on the canvas
  rocket.x = 32;
  rocket.y = 32;

  //Add the rocket to the stage
  stage.addChild(rocket);
  
  //Render the stage   
  renderer.render(stage);
}
```
Pixi的内置对象`Rectangle`(PIXI.Rectangle）定义了一个矩形对象，第一个参数 x 位置，第二个参数 y 位置，第三个为宽度 width，第四个为高度 height

```js
var rectangle = new PIXI.Rectangle(x, y, width, height);
```
texture 纹理对象设置 frame属性为Rectangle就可以在纹理texture中裁剪一个子图像

```js
var rectangle = new Rectangle(192, 128, 64, 64);
texture.frame = rectangle;
```

```js
var rocket = new Sprite(texture);
```
明白它的工作原理了吧？
这样使用的话也很麻烦，因为要不停的声明裁剪的位置和大小，接下来，我们介绍另外一种方法（json 定义）

<a id='textureatlas'></a>

定义一个‘纹理’的集合（理解为使用定义好的 json 文件或者对象来制作）
---------------------

如果你使用 Pixi 来构建大型的应用和游戏，那么你需要一个有效的方法和数据集合来声明tilesets，这里说的数据即为 json，json 对象包含了子图像的位置、大小。这意味着可以解耦您的程序，需要改变游戏、应用属性，只需要更改 json 数据就可以了。利用数据来显示正确的图像，而不去更改代码。

Pixi 兼容 JSON 格式的数据，可以使用[Texture Packer](https://www.codeandweb.com/texturepacker)来生成texture atlas(纹理瓦片集合),更简洁的工具：[Shoebox](http://renderhjs.net/shoebox/) 或者 [spritesheet.js](https://github.com/krzysztof-o/spritesheet.js/)，来导出 PNG 和 JSON 定义的 Pixi 兼容的文件。

从个人收藏的图像创建：[点击查看更多示例](http://opengameart.org/users/sharm)
打开Texture Packer（从https://www.codeandweb.com/texturepacker上下载），选择 JSON HASH作为基础格式，拖动你所选则的图像到工作区 workspace，也可以按照文件夹导入图像。

(如果你使用的是Texture Packer免费版, 设置 **Algorithm** 为`Basic`, **Trim mode** 为
`None`, **Size constraints** 为 `Any size` 并且设置 **PNG Opt
Level** 最小值 `0`. 这些设置保证在使用免费版时候不会报错)

制作完成后，点击**Publish**按钮，选择文件名称和地址，并保存。你可以得到两个文件：一个 PNG ，一个 JSON 文件。问了让开发更容易，可以保持这两个文件都在同一个文件夹下（image 文件夹）,json 文件描述了各个子图像的大小、位置信息，格式如下：

```js
"blob.png":
{
	"frame": {"x":55,"y":2,"w":32,"h":24},
	"rotated": false,
	"trimmed": false,
	"spriteSourceSize": {"x":0,"y":0,"w":32,"h":24},
	"sourceSize": {"w":32,"h":24},
	"pivot": {"x":0.5,"y":0.5}
},
```
The `treasureHunter.json` file also contains “dungeon.png”,
“door.png”, "exit.png", and "explorer.png" properties each with
similar data. Each of these sub-images are called **frames**. Having
this data is really helpful because now you don’t need to know the
size and position of each sub-image in the tileset. All you need to
know is the sprite’s **frame id**. The frame id is just the name
of the original image file, like "blob.png" or "explorer.png".

Among the many advantages to using a texture atlas is that you can
easily add 2 pixels of padding around each image (Texture Packer does
this by default.) This is important to prevent the possibility of
**texture bleed**. Texture bleed is an effect that happens when the
edge of an adjacent image on the tileset appears next to a sprite.
This happens because of the way your computer's GPU (Graphics
Processing Unit) decides how to round fractional pixels values. Should
it round them up or down? This will be different for each GPU.
Leaving 1 or 2 pixels spacing around images on a tilseset makes all
images display consistently.

(Note: If you have two pixels of padding around a graphic, and you still notice a strange "off by one pixel" glitch in the
way Pixi is displaying it, try changing the texture's scale mode
algorithm. Here's how: `texture.baseTexture.scaleMode =
PIXI.SCALE_MODES.NEAREST;`. These glitches can sometimes happen
because of GPU floating point rounding errors.)

Now that you know how to create a texture atlas, let's find out how to
load it into your game code.

<a id='loadingatlas'></a>
加载’纹理‘集合
-------------------------

To get the texture atlas into Pixi, load it using Pixi’s
`loader`. If the JSON file was made with Texture Packer, the
`loader` will interpret the data and create a texture from each
frame on the tileset automatically.  Here’s how to use the `loader` to load the `treasureHunter.json`
file. When it has loaded, the `setup` function will run.
```js
loader
  .add("images/treasureHunter.json")
  .load(setup);
```
Each image on the tileset is now an individual texture in Pixi’s
cache. You can access each texture in the cache with the same name it
had in Texture Packer (“blob.png”, “dungeon.png”, “explorer.png”,
etc.).

<a id='creatingsprites'></a>
使用一个定义了‘纹理’的集合创建精灵
--------------------------------------------

Pixi gives you three general ways to create a sprite from a texture atlas:

1.	Using `TextureCache`:
```js
var texture = TextureCache["frameId.png"],
    sprite = new Sprite(texture);
```
2.	If you’ve used Pixi’s `loader` to load the texture atlas, use the 
loader’s `resources`:
```js
var sprite = new Sprite(
  resources["images/treasureHunter.json"].textures["frameId.png"]
);
```
3. That’s way too much to typing to have to do just to create a sprite! 
So I suggest you create an alias called `id` that points to texture’s 
altas’s `textures` object, like this:
```js
var id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
```
Then you can just create each new sprite like this:
```js
let sprite = new Sprite(id["frameId.png"]);
```
Much better!

Here's how you could use these three different sprite creation
techniques in the `setup` function to create and display the
`dungeon`, `explorer`, and `treasure` sprites.
```js
//Define variables that might be used in more 
//than one function
var dungeon, explorer, treasure, door, id;

function setup() {

  //There are 3 ways to make sprites from textures atlas frames

  //1. Access the `TextureCache` directly
  var dungeonTexture = TextureCache["dungeon.png"];
  dungeon = new Sprite(dungeonTexture);
  stage.addChild(dungeon);

  //2. Access the texture using throuhg the loader's `resources`:
  explorer = new Sprite(
    resources["images/treasureHunter.json"].textures["explorer.png"]
  );
  explorer.x = 68;

  //Center the explorer vertically
  explorer.y = stage.height / 2 - explorer.height / 2;
  stage.addChild(explorer);

  //3. Create an optional alias called `id` for all the texture atlas 
  //frame id textures.
  id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
  
  //Make the treasure box using the alias
  treasure = new Sprite(id["treasure.png"]);
  stage.addChild(treasure);

  //Position the treasure next to the right edge of the canvas
  treasure.x = stage.width - treasure.width - 48;
  treasure.y = stage.height / 2 - treasure.height / 2;
  stage.addChild(treasure);


  //Render the stage
  renderer.render(stage);
}
```
Here's what this code displays:

![Explorer, dungeon and treasure](/examples/images/screenshots/13.png)

The stage dimensions are 512 by 512 pixels, and you can see in the
code above that the `stage.height` and `stage.width` properties are used
to align the sprites. Here's how the `explorer`'s `y` position is
vertically centered:
```js
explorer.y = stage.height / 2 - explorer.height / 2;
```
Learning to create and display sprites using a texture atlas is an
important benchmark. So before we continue, let's take a look at the
code you
could write to add the remaining
sprites: the `blob`s and `exit` door, so that you can produce a scene
that looks like this:

![All the texture atlas sprites](/examples/images/screenshots/14.png)

Here's the entire code that does all this. I've also included the HTML
code so you can see everything in its proper context.
(You'll find this working code in the
`examples/spriteFromTextureAtlas.html` file in this repository.)
Notice that the `blob` sprites are created and added to the stage in a
loop, and assigned random positions.
```js
<!doctype html>
<meta charset="utf-8">
<title>Make a sprite from a texture atlas</title>
<body>
<script src="../pixi.js/bin/pixi.js"></script>
<script>

//Aliases
var Container = PIXI.Container,
    autoDetectRenderer = PIXI.autoDetectRenderer,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    TextureCache = PIXI.utils.TextureCache,
    Texture = PIXI.Texture,
    Sprite = PIXI.Sprite;

//Create a Pixi stage and renderer and add the 
//renderer.view to the DOM
var stage = new Container(),
    renderer = autoDetectRenderer(512, 512);
document.body.appendChild(renderer.view);

//load a JSON file and run the `setup` function when it's done
loader
  .add("images/treasureHunter.json")
  .load(setup);

//Define variables that might be used in more 
//than one function
var dungeon, explorer, treasure, door, id;

function setup() {

  //There are 3 ways to make sprites from textures atlas frames

  //1. Access the `TextureCache` directly
  var dungeonTexture = TextureCache["dungeon.png"];
  dungeon = new Sprite(dungeonTexture);
  stage.addChild(dungeon);

  //2. Access the texture using throuhg the loader's `resources`:
  explorer = new Sprite(
    resources["images/treasureHunter.json"].textures["explorer.png"]
  );
  explorer.x = 68;

  //Center the explorer vertically
  explorer.y = stage.height / 2 - explorer.height / 2;
  stage.addChild(explorer);

  //3. Create an optional alias called `id` for all the texture atlas 
  //frame id textures.
  id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
  
  //Make the treasure box using the alias
  treasure = new Sprite(id["treasure.png"]);
  stage.addChild(treasure);

  //Position the treasure next to the right edge of the canvas
  treasure.x = stage.width - treasure.width - 48;
  treasure.y = stage.height / 2 - treasure.height / 2;
  stage.addChild(treasure);

  //Make the exit door
  door = new Sprite(id["door.png"]); 
  door.position.set(32, 0);
  stage.addChild(door);

  //Make the blobs
  var numberOfBlobs = 6,
      spacing = 48,
      xOffset = 150;

  //Make as many blobs as there are `numberOfBlobs`
  for (var i = 0; i < numberOfBlobs; i++) {

    //Make a blob
    var blob = new Sprite(id["blob.png"]);

    //Space each blob horizontally according to the `spacing` value.
    //`xOffset` determines the point from the left of the screen
    //at which the first blob should be added.
    var x = spacing * i + xOffset;

    //Give the blob a random y position
    //(`randomInt` is a custom function - see below)
    var y = randomInt(0, stage.height - blob.height);

    //Set the blob's position
    blob.x = x;
    blob.y = y;

    //Add the blob sprite to the stage
    stage.addChild(blob);
  }

  //Render the stage   
  renderer.render(stage);
}

//The `randomInt` helper function
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

</script>
</body>
```
You can see in the code above that all the blobs are created using a
`for` loop. Each `blob` is spaced evenly along the `x` axis like this:
```js
var x = spacing * i + xOffset;
blob.x = x;
```
`spacing` has a value 48, and `xOffset` has a value of 150. What this
means that that the first `blob` will have an `x` position of 150.
This offsets it from the left side of the stage by 150 pixel. Each
subsequent `blob` will have an `x` value that's 48 pixels greater than
the `blob` created in the previous iteration of the loop. This creates
an evenly spaced line of blob monsters, from left to right, along the dungeon floor.

Each `blob` is also given a random `y` position. Here's the code that
does this:
```js
var y = randomInt(0, stage.height - blob.height);
blob.y = y;
```
The `blob`'s `y` position could be assigned any random number between 0 and
512, which is the value of `stage.height`. This works with the help of
a custom function called `randomInt`. `randomInt` returns a random number
that's within a range between any two numbers you supply.
```js
randomInt(lowestNumber, highestNumber)
```
That means if you want a random number between 1 and 10, you can get
one like this:
```js
var randomNumber = randomInt(1, 10);
```
Here's the `randomInt` function definition that does all this work:
```js
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
```
`randomInt` is a great little function to keep in your back pocket for
making games - I use it all the time.

<a id='movingsprites'></a>
移动精灵
--------------

移动一个精灵很方便。我们将会使用 `requestAnimationFrame` 制作一个循环，这叫做 **game loop**
每隔一秒，可以控制精灵移动1px,每秒60帧

```js
function gameLoop() {

  //Loop this function at 60 frames per second
  requestAnimationFrame(gameLoop);

  //Move the cat 1 pixel to the right each frame
  cat.x += 1;

  //Render the stage to see the animation
  renderer.render(stage);
}

//Start the game loop
gameLoop();
```

如果希望精灵往相反的方向移动，只需要将 x 或者 y 轴的数字递减 -1 就可以了。

```js
//Aliases
var Container = PIXI.Container,
    autoDetectRenderer = PIXI.autoDetectRenderer,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    Sprite = PIXI.Sprite;

//Create a Pixi stage and renderer 
var stage = new Container(),
    renderer = autoDetectRenderer(256, 256);
document.body.appendChild(renderer.view);

//Load an image and the run the `setup` function
loader
  .add("images/cat.png")
  .load(setup);

//Define any variables that are used in more than one function
var cat;

function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  cat.y = 96; 
  stage.addChild(cat);
 
  //Start the game loop
  gameLoop();
}

function gameLoop(){

  //Loop this function 60 times per second
  requestAnimationFrame(gameLoop);

  //Move the cat 1 pixel per frame
  cat.x += 1;

  //Render the stage
  renderer.render(stage);
}
```

<a id='velocity'></a>
使用精灵的‘速度’属性
-------------------------

为了更好控制动画播放，pixi 提供了`velocity properties` `vx` `vy`分别控制 x 轴、y 轴的移动速度，初始值`vx` 和 `vy`为0，代表不移动；

```js
cat.vx = 0;
cat.vy = 0;
```
接下来你想如何移动呢？

```js
function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  stage.addChild(cat);

  //Initialize the cat's velocity variables
  cat.vx = 0;
  cat.vy = 0;
 
  //Start the game loop
  gameLoop();
}

function gameLoop(){

  //Loop this function 60 times per second
  requestAnimationFrame(gameLoop);

  //Update the cat's velocity
  cat.vx = 1;
  cat.vy = 1;

  //Apply the velocity values to the cat's 
  //position to make it move
  cat.x += cat.vx;
  cat.y += cat.vy;

  //Render the stage
  renderer.render(stage);
}


```

改变`vx` `vy`为负值，可以向相反的方向移动；也可以配合鼠标、键盘使用。


<a id='gamestates'></a>
Game states
-----------

模块化开发建议：

```js
//默认设置游戏状态为play
var state = play;

function gameLoop() {
  requestAnimationFrame(gameLoop);
  state();
  renderer.render(stage);
}

function play() {
  cat.x += 1;
}
```

以上代码代表，每秒调用60次，state = play;
重构下以前的代码：

```js
//全局定义 sprite 精灵、精灵动画
var cat, state;

function setup() {
  cat = new Sprite(resources["images/cat.png"].texture);
  cat.y = 96; 
  cat.vx = 0;
  cat.vy = 0;
  stage.addChild(cat);
  state = play;
  gameLoop();
}

function gameLoop(){
  requestAnimationFrame(gameLoop);
  state();
  renderer.render(stage);
}

//x 轴递增，向右运动
function play() {
  cat.vx = 1
  cat.x += cat.vx;
}
```

<a id='keyboard'></a>
键盘事件
-----------------

这里，我们建立一个键盘事件来控制精灵，达到监听和控制精灵的效果。

```js
function keyboard(keyCode) {
  var key = {};
  key.code = keyCode;
  key.isDown = false;
  key.isUp = true;
  key.press = undefined;
  key.release = undefined;
  //The `downHandler`
  key.downHandler = function(event) {
    if (event.keyCode === key.code) {
      if (key.isUp && key.press) key.press();
      key.isDown = true;
      key.isUp = false;
    }
    event.preventDefault();
  };

  //The `upHandler`
  key.upHandler = function(event) {
    if (event.keyCode === key.code) {
      if (key.isDown && key.release) key.release();
      key.isDown = false;
      key.isUp = true;
    }
    event.preventDefault();
  };

  //Attach event listeners
  window.addEventListener(
    "keydown", key.downHandler.bind(key), false
  );
  window.addEventListener(
    "keyup", key.upHandler.bind(key), false
  );
  return key;
}
```

keyboard 方法很易用，可以像这样传建一个键盘对象

```js
var keyObject = keyboard(asciiKeyCodeNumber);
```

asciiKeyCodeNumber 是指 Key Code Values。[点击这里查看Key Code Values](http://help.adobe.com/en_US/AS2LCR/Flash_10.0/help.html?content=00000520.html).

Then assign `press` and `release` methods to the keyboard object like this:
```js
keyObject.press = function() {
  //key object pressed
};
keyObject.release = function() {
  //key object released
};
```
Keyboard objects also have `isDown` and `isUp` Boolean properties that
you can use to check the state of each key.

Take a look at the
`keyboardMovement.html` file in the `examples` folder to see how you
can use this `keyboard` function to control a sprite using your
keyboard's arrow keys. Run it and use the left, up, down, and right
arrow keys to move the cat around the stage.

![Keyboard movement](/examples/images/screenshots/17.png)

Here's the code that does all this:
```js
function setup() {

  //Create the `cat` sprite
  cat = new Sprite("images/cat.png");
  cat.y = 96;
  cat.vx = 0;
  cat.vy = 0;
  stage.addChild(cat);

  //Capture the keyboard arrow keys
  var left = keyboard(37),
      up = keyboard(38),
      right = keyboard(39),
      down = keyboard(40);

  //Left arrow key `press` method
  left.press = function() {

    //Change the cat's velocity when the key is pressed
    cat.vx = -5;
    cat.vy = 0;
  };

  //Left arrow key `release` method
  left.release = function() {

    //If the left arrow has been released, and the right arrow isn't down,
    //and the cat isn't moving vertically:
    //Stop the cat
    if (!right.isDown && cat.vy === 0) {
      cat.vx = 0;
    }
  };

  //Up
  up.press = function() {
    cat.vy = -5;
    cat.vx = 0;
  };
  up.release = function() {
    if (!down.isDown && cat.vx === 0) {
      cat.vy = 0;
    }
  };

  //Right
  right.press = function() {
    cat.vx = 5;
    cat.vy = 0;
  };
  right.release = function() {
    if (!left.isDown && cat.vy === 0) {
      cat.vx = 0;
    }
  };

  //Down
  down.press = function() {
    cat.vy = 5;
    cat.vx = 0;
  };
  down.release = function() {
    if (!up.isDown && cat.vx === 0) {
      cat.vy = 0;
    }
  };

  //Set the game state
  state = play;

  //Start the game loop
  gameLoop();
}

function gameLoop() {
  requestAnimationFrame(gameLoop);
  state();
  renderer.render(stage);
}

function play() {

  //Use the cat's velocity to make it move
  cat.x += cat.vx;
  cat.y += cat.vy
}
```
<a id='grouping'></a>
Grouping Sprites
----------------

Groups let you create game scenes, and manage similar sprites together
as single units. Pixi has an object called a `Container`
that lets you do this. Let's find out how it works.

Imagine that you want to display three sprites: a cat, hedgehog and
tiger. Create them, and set their positions - *but don't add them to the
stage*.
```js
//The cat
var cat = new Sprite(id["cat.png"]);
cat.position.set(16, 16);

//The hedgehog
var hedgehog = new Sprite(id["hedgehog.png"]);
hedgehog.position.set(32, 32);

//The tiger
var tiger = new Sprite(id["tiger.png"]);
tiger.position.set(64, 64);
```

Next, create an `animals` container to group them all together like
this:
```js
var animals = new Container();
```
Then use `addChild` to *add the sprites to the group*.
```js
animals.addChild(cat);
animals.addChild(hedgehog);
animals.addChild(tiger);
```
Finally add the group to the stage.
```js
stage.addChild(animals);
renderer.render(stage);
```
(As you know, the `stage` object is also a `Container`. It’s the root
container for all Pixi sprites.)

Here's what this code produces:

![Grouping sprites](/examples/images/screenshots/18.png)

What you can't see in that image is the invisible `animals` group
that's containing the sprites.

![Grouping sprites](/examples/images/screenshots/19.png)

You can now treat the `animals` group as a single unit. You can think
of a `Container` as a special kind of sprite that doesn’t
have a texture.

If you need a list of all the child sprites that `animals` contains,
use its `children` array to find out.
```
console.log(animals.chidren}
//Displays: Array [Object, Object, Object]
```
This tells you that `animals` has three sprites as children.

Because the `animals` group is just like any other sprite, you can
change its `x` and `y` values, `alpha`, `scale` and
all the other sprite properties. Any property value you change on the
parent container will affect the child sprites in a relative way. So if you
set the group's `x` and `y` position, all the child sprites will
be repositioned relative to the group's top left corner. What would
happen if you set the `animals`'s `x` and `y` position to 64?
```
animals.position.set(64, 64);
```
The whole group of sprites will move 64 pixels right and 64 pixels to
the down.

![Grouping sprites](/examples/images/screenshots/20.png)

The `animals` group also has its own dimensions, which is based on the area
occupied by the containing sprites. You can find its `width` and
`height` values like this:
```js
console.log(animals.width);
//Displays: 112

console.log(animals.height);
//Displays: 112

```
![Group width and height](/examples/images/screenshots/21.png)

What happens if you change a group's width or height?
```js
animals.width = 200;
animals.height = 200;
```
All the child
sprites will scale to match that change.

![Group width and height](/examples/images/screenshots/22.png)

You can nest as many `Container`s inside other
`Container`s as you like, to create deep hierarchies if
you need to. However, a `DisplayObject` (like a `Sprite` or another
`Container`) can only belong to one parent at a time. If
you use `addChild` to make a sprite the child of another object, Pixi
will automatically remove it from its current parent. That’s a useful
bit of management that you don’t have to worry about.

<a id='localnglobal'></a>
###Local and global positions

When you add a sprite to a `Container`, its `x` and `y`
position is *relative to the group’s top left corner*. That's the
sprite's **local position** For example, what do you think the cat's
position is in this image?

![Grouping sprites](/examples/images/screenshots/20.png)

Let's find out:
```
console.log(cat.x);
//Displays: 16
```
16? Yes! That's because the cat is offset by only 16 pixel's from the
group's top left corner. 16 is the cat's local position.

Sprites also have a **global position**. The global position is the
distance from the top left corner of the stage, to the sprite's anchor
point (usually the sprite's top left corner.) You can find a sprite's global
position with the help of the `toGlobal` method.  Here's how:
```
parentSprite.toGlobal(childSprite.position)
```
That means you can find the cat's global position inside the `animals`
group like this:
```
console.log(animals.toGlobal(cat.position));
//Displays: Object {x: 80, y: 80...};
```
That gives you an `x` and `y` position of 80. That's exactly the cat's
global position relative to the top left corner of the stage. 

What if you want to find the global position of a sprite, but don't
know what the sprite's parent container
is? Every sprite has a property called `parent` that will tell you what the
sprite's parent is. If you add a sprite directly to the `stage`, then
`stage` will be the sprite's parent. In the example above, the `cat`'s
parent is `animals`. That means you can alternatively get the cat's global position
by writing code like this:
```
cat.parent.toGlobal(cat.position);
```
And it will work even if you don't know what the cat's parent
container currently is.

There's one more way to calculate the global position! And, it's
actually the best way, so heads up! If you want to know the distance
from the top left corner of the canvas to the sprite, and don't know
or care what the sprite's parent containers are, use the
`getGlobalPosition` method. Here's how to use it to find the tiger's global position:
```js
tiger.getGlobalPosition().x
tiger.getGlobalPosition().y
```
This will give you `x` and `y` values of 128 in the example that we've
been using.
The special thing about `getGlobalPosition` is that it's highly
precise: it will give you the sprite's accurate global position as
soon as its local position changes. I asked the Pixi development team
to add this feature specifically for accurate collision detection for
games.

What if you want to convert a global position to a local position? you
can use the `toLocal` method. It works in a similar way, but uses this
general format:
```js
sprite.toLocal(sprite.position, anyOtherSprite)
```
Use `toLocal` to find the distance between a sprite and any other
sprite. Here's how you could find out the tiger's local
position, relative to the hedgehog.
```js
tiger.toLocal(tiger.position, hedgehog).x
tiger.toLocal(tiger.position, hedgehog).y
```
This gives you an `x` value of 32 and a `y` value of 32. You can see
in the example images that the tiger's top left corner is 32 pixels
down and to the left of the hedgehog's top left corner.

<a id='spritebatch'></a>
###Using a ParticleContainer to group sprites

Pixi has an alternative, high-performance way to group sprites called
a `ParticleContainer` (`PIXI.ParticleContainer`). Any sprites inside a
`ParticleContainer` will render 2 to 5
times faster than they would if they were in a regular
`Container`. It’s a great performance boost for games.

Create a `ParticleContainer` like this:
```js
var superFastSprites = new ParticleContainer();
```
Then use `addChild` to add sprites to it, just like you would with any
ordinary `Container`.

You have to make some compromises if you decide to use a
`ParticleContainer`. Sprites inside a `ParticleContainer` only have a few  basic properties:
`x`, `y`, `width`, `height`, `scale`, `pivot`, `alpha`, `visible` – and that’s
about it. Also, the sprites that it contains can’t have nested
children of their own. A `ParticleContainer` also can’t use Pixi’s advanced
visual effects like filters and blend modes. But for the huge performance boost that you get, those
compromises are usually worth it. And you can use
`Container`s and `ParticleContainer`s simultaneously in the same project, so you can fine-tune your optimization.

Why are sprites in a `Particle Container` so fast? Because the positions of
the sprites are being calculated directly on the GPU. The Pixi
development team is working to offload as much sprite processing as
possible on the GPU, so it’s likely that the latest version of Pixi
that you’re using will have much more feature-rich `ParticleContainer` than
what I've described here. Check the current [`ParticleContainer`
documentation](http://pixijs.github.io/docs/PIXI.ParticleContainer.html) for details.

Where you create a `ParticleContainer`, there are two optional
arguments you can provide: the maximum number of sprites the container
can hold, and an options object.
```js
var superFastSprites = new ParticleContainer(size, options);
```
The default value for size is 15,000. So, if you need to contain more
sprites, set it to a higher number. The options argument is an object
with 5 Boolean values you can set: `scale`, `position`, `rotation`, `uvs` and
`alpha`. The default value of `position` is `true`, but all the others
are set to `false`. That means that if you want change the `rotation`,
`scale`, `alpha`, or `uvs` of sprite in the `ParticleContainer`, you
have to set those properties to `true`, like this:
```js
var superFastSprites = new ParticleContainer(
  size, 
  {
    rotation: true,
    alpha: true,
    scale: true,
    uvs: true
  }
);
```
But, if you don't think you'll need to use these properties, keep them
set to `false` to squeeze out the maximum amount of performance.

What's the `uvs` option? Only set it to `true` if you have particles
which change their textures while they're being animated. (All the
sprite's textures will also need to be on the same tileset image for
this to work.) 

(Note: **UV mapping** is a 3D graphics display term that refers to
the `x` and `y` coordinates of the texture (the image) that is being
mapped onto a 3D surface. `U` is the `x` axis and `V` is the `y` axis.
WebGL already uses `x`, `y` and `z` for 3D spatial positioning, so `U`
and `V` were chosen to represent `x` and `y` for 2D image textures.)

<a id='graphic'></a>
Pixi's Graphic Primitives
-------------------------

Using image textures is one of the most useful ways of making sprites,
but Pixi also has its own low-level drawing tools. You can use them to
make rectangles, shapes, lines, complex polygons and text. And,
fortunately, it uses almost the same API as the [Canvas Drawing API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Drawing_graphics_with_canvas) so,
if you're already familiar with canvas, here’s nothing really new to
  learn. But the big advantage is that, unlike the Canvas Drawing API,
  the shapes you draw with Pixi are rendered by WebGL on the GPU. Pixi
  lets you access all that untapped performance power.
Let’s take a quick tour of how to make some basic shapes. Here are all
the shapes we'll make in the code ahead.

![Graphic primitives](/examples/images/screenshots/23.png)

<a id='rectangles'></a>
###Rectangles

All shapes are made by first creating a new instance of Pixi's
`Graphics` class (`PIXI.Graphics`).
```js
var rectangle = new Graphics();
```
Use `beginFill` with a hexadecimal color code value to set the
rectangle’ s fill color. Here’ how to set to it to light blue.
```js
rectangle.beginFill(0x66CCFF);
```
If you want to give the shape an outline, use the `lineStyle` method. Here's
how to give the rectangle a 4 pixel wide red outline, with an `alpha`
value of 1.
```js
rectangle.lineStyle(4, 0xFF3300, 1);
```
Use the `drawRect` method to draw the rectangle. Its four arguments
are `x`, `y`, `width` and `height`.
```js
rectangle.drawRect(x, y, width, height);
```
Use `endFill` when you’re done.
```js
rectangle.endFill();
```
It’s just like the Canvas Drawing API! Here’s all the code you need to
draw a rectangle, change its position, and add it to the stage.
```js
var rectangle = new Graphics();
rectangle.lineStyle(4, 0xFF3300, 1);
rectangle.beginFill(0x66CCFF);
rectangle.drawRect(0, 0, 64, 64);
rectangle.endFill();
rectangle.x = 170;
rectangle.y = 170;
stage.addChild(rectangle);

```
This code makes a 64 by 64 blue rectangle with a red border at an x and y position of 170.

<a id='circles'></a>
###Circles

Make a circle with the `drawCircle` method. Its three arguments are
`x`, `y` and `radius`
```js
drawCircle(x, y, radius)
```
Unlike rectangles and sprites, a circle’s x and y position is also its
center point. Here’s how to make a violet colored circle with a radius of 32 pixels.
```js
var circle = new Graphics();
circle.beginFill(0x9966FF);
circle.drawCircle(0, 0, 32);
circle.endFill();
circle.x = 64;
circle.y = 130;
stage.addChild(circle);
```
<a id='ellipses'></a>
###Ellipses
As a one-up on the Canvas Drawing API, Pixi lets you draw an ellipse
with the `drawEllipse` method.
```js
drawEllipse(x, y, width, height);
```
The x/y position defines the ellipse’s top left corner (imagine that
the ellipse is surrounded by an invisible rectangular bounding box -
the top left corner of that box will represent the ellipse's x/y
anchor position). Here’s a yellow ellipse that’s 50 pixels wide and 20 pixels high.
```js
var ellipse = new Graphics();
ellipse.beginFill(0xFFFF00);
ellipse.drawEllipse(0, 0, 50, 20);
ellipse.endFill();
ellipse.x = 180;
ellipse.y = 130;
stage.addChild(ellipse);
```
<a id='roundedrect'></a>
###Rounded rectangles

Pixi also lets you make rounded rectangles with the `drawRoundedRect`
method. The last argument, `cornerRadius` is a number in pixels that
determines by how much the corners should be rounded.
```js
drawRoundedRect(x, y, width, height, cornerRadius)
```
Here's how to make a rounded rectangle with a corner radius of 10
pixels.
```js
var roundBox = new Graphics();
roundBox.lineStyle(4, 0x99CCFF, 1);
roundBox.beginFill(0xFF9933);
roundBox.drawRoundedRect(0, 0, 84, 36, 10)
roundBox.endFill();
roundBox.x = 48;
roundBox.y = 190;
stage.addChild(roundBox);
```
<a id='lines'></a>
###Lines

You've seen in the examples above that the `lineStyle` method lets you
define a line.  You can use the `moveTo` and `lineTo` methods to draw the
start and end points of the line, in just the same way you can with the Canvas
Drawing API. Here’s how to draw a 4 pixel wide, white diagonal line.
```js
var line = new Graphics();
line.lineStyle(4, 0xFFFFFF, 1);
line.moveTo(0, 0);
line.lineTo(80, 50);
line.x = 32;
line.y = 32;
stage.addChild(line);
```
`PIXI.Graphics` objects, like lines, have `x` and `y` values, just
like sprites, so you can position them anywhere on the stage after
you've drawn them.

<a id='polygons'></a>
###Polygons

You can join lines together and fill them with colors to make complex
shapes using the `drawPolygon` method. `drawPolygon`'s argument is an
path array of x/y points that define the positions of each point on the
shape.
```js
var path = [
  point1X, point1Y,
  point2X, point2Y,
  point3X, point3Y
];

graphicsObject.drawPolygon(path);
```
`drawPolygon` will join those three points together to make the shape.
Here’s how to use `drawPolygon` to connect three lines together to
make a red triangle with a blue border. The triangle is drawn at
position 0,0 and then moved to its position on the stage using its
`x` and `y` properties.
```js
var triangle = new Graphics();
triangle.beginFill(0x66FF33);

//Use `drawPolygon` to define the triangle as
//a path array of x/y positions

triangle.drawPolygon([
    -32, 64,             //First point
    32, 64,              //Second point
    0, 0                 //Third point
]);

//Fill shape's color
triangle.endFill();

//Position the triangle after you've drawn it.
//The triangle's x/y position is anchored to its first point in the path
triangle.x = 180;
triangle.y = 22;

stage.addChild(triangle);
```
<a id='text'></a>
Displaying text
---------------

Use a `Text` object (`PIXI.Text`) to display text on the stage. The constructor
takes two arguments: the text you want to display and a style object
that defines the font’s properties. Here's how to display the words
"Hello Pixi", in white, 32 pixel high sans-serif font.
```js
var message = new Text(
  "Hello Pixi!",
  {font: "32px sans-serif", fill: "white"}
);

message.position.set(54, 96);
stage.addChild(message);
```
![Displaying text](/examples/images/screenshots/24.png)

Pixi’s Text objects inherit from the `Sprite` class, so they
contain all the same properties like `x`, `y`, `width`, `height`,
`alpha`, and `rotation`. Position and resize text on the stage just like you would any other sprite.

If you want to change the content of a text object after you've
created it, use the `text` property.
```js
message.text = "Text changed!";
```
Use the `style` property if you want to redefine the font properties.
```js
message.style = {fill: "black", font: "16px PetMe64"};
```
Pixi makes text objects by using the Canvas Drawing API to
render the text to an invisible and temporary canvas
element. It then turns the canvas into a WebGL texture so that it
can be mapped onto a sprite. That’s why the text’s color needs to be
wrapped in a string: it’s a Canvas Drawing API color value. As with
any canvas color values, you can use words for common colors like
“red” or “green”, or use rgba, hsla or hex values.

Other style properties that you can include are `stroke` for the font
outline color and `strokeThickness` for the outline thickness. Set the
text's `dropShadow` property to `true` to make the text display a
shadow. Use `dropShadowColor` to set the shadow's hexadecimal color
value, use `dropShadowAngle` to set the shadow's angle in radians, and
use `dropShadowDistance` to set the pixel height of a shadow. And
there's more: [check out Pixi's Text documentation for the full
list](http://pixijs.github.io/docs/PIXI.Text.html).

Pixi can also wrap long lines of text. Set the text’s `wordWrap` style
property to `true`, and then set `wordWrapWidth` to the maximum length
in pixels, that the line of text should be. Use the `align` property
to set the alignment for multi-line text.
```js
message.style = {wordWrap: true, wordWrapWidth: 100, align: center};
```
(Note: `align` doesn't affect single line text.)

If you want to use a custom font file, use the CSS `@font-face` rule
to link the font file to the HTML page where your Pixi application is
running.
```js
@font-face {
  font-family: "fontFamilyName";
  src: url("fonts/fontFile.ttf");
}
```
Add this `@font-face` rule to your HTML page's CSS style sheet.

[Pixi also has support for bitmap
fonts](http://pixijs.github.io/docs/PIXI.extras.BitmapText.html). You
can use Pixi's loader to load Bitmap font XML files, the same way you
load JSON or image files.

<a id='collision'></a>
Collision detection
--------------------------

You now know how to make a huge variety of graphics objects, but what
can you do with them? A fun thing to do is to build a simple **collision
detection** system. You can use a custom function called
`hitTestRectangle` that checks whether any two rectangular Pixi sprites are
touching.
```js
hitTestRectangle(spriteOne, spriteTwo)
```
if they overlap, `hitTestRectangle` will return `true`. You can use `hitTestRectangle` with an `if` statement to check for a collision between two sprites like this:
```js
if (hitTestRectangle(cat, box)) {
  //There's a collision
} else {
  //There's no collision
}
```
As you'll see, `hitTestRectangle` is the front door into the vast universe of game design.

Run the `collisionDetection.html` file in the `examples` folder for a
working example of how to use `hitTestRectangle`. Use the arrow keys
to move the cat. If the cat hits the box, the box becomes red
and "Hit!" is displayed by the text object.

![Displaying text](/examples/images/screenshots/25.png)

You've already seen all the code that creates all these elements, as
well as the
keyboard control system that makes the cat move. The only new thing is the
way `hitTestRectangle` is used inside the `play` function to check for a
collision.
```js
function play() {

  //use the cat's velocity to make it move
  cat.x += cat.vx;
  cat.y += cat.vy;

  //check for a collision between the cat and the box
  if (hitTestRectangle(cat, box)) {

    //if there's a collision, change the message text
    //and tint the box red
    message.text = "hit!";
    box.tint = 0xff3300;

  } else {

    //if there's no collision, reset the message
    //text and the box's color
    message.text = "No collision...";
    box.tint = 0xccff99;
  }
}
```
Because the `play` function is being called by the game loop 60 times
per second, this `if` statement is constantly checking for a collision
between the cat and the box. If `hitTestRectangle` is `true`, the
text `message` object uses `setText` to display "Hit":
```js
message.text = "hit!";
```
The color of the box is then changed from green to red by setting the
box's `tint` property to the hexadecimal red value.
```js
box.tint = 0xff3300;
```
If there's no collision, the message and box are maintained in their
original states:
```js
message.text = "no collision...";
box.tint = 0xccff99;
```
This code is pretty simple, but suddenly you've created an interactive
world that seems to be completely alive. It's almost like magic! And, perhaps
surprisingly, you now have all the skills you need to start making
games with Pixi!

<a id='hittest'></a>
###The hitTestRectangle function

But what about the `hitTestRectangle` function? What does it do, and
how does it work? The details of how collision detection algorithms
like this work is a little bit outside the scope of this tutorial.
The most important thing is that you know how to use it. But, just for
your reference, and in case you're curious, here's the complete
`hitTestRectangle` function definition. Can you figure out from the
comments what it's doing?
```js
function hitTestRectangle(r1, r2) {

  //Define the variables we'll need to calculate
  var hit, combinedHalfWidths, combinedHalfHeights, vx, vy;

  //hit will determine whether there's a collision
  hit = false;

  //Find the center points of each sprite
  r1.centerX = r1.x + r1.width / 2;
  r1.centerY = r1.y + r1.height / 2;
  r2.centerX = r2.x + r2.width / 2;
  r2.centerY = r2.y + r2.height / 2;

  //Find the half-widths and half-heights of each sprite
  r1.halfWidth = r1.width / 2;
  r1.halfHeight = r1.height / 2;
  r2.halfWidth = r2.width / 2;
  r2.halfHeight = r2.height / 2;

  //Calculate the distance vector between the sprites
  vx = r1.centerX - r2.centerX;
  vy = r1.centerY - r2.centerY;

  //Figure out the combined half-widths and half-heights
  combinedHalfWidths = r1.halfWidth + r2.halfWidth;
  combinedHalfHeights = r1.halfHeight + r2.halfHeight;

  //Check for a collision on the x axis
  if (Math.abs(vx) < combinedHalfWidths) {

    //A collision might be occuring. Check for a collision on the y axis
    if (Math.abs(vy) < combinedHalfHeights) {

      //There's definitely a collision happening
      hit = true;
    } else {

      //There's no collision on the y axis
      hit = false;
    }
  } else {

    //There's no collision on the x axis
    hit = false;
  }

  //`hit` will be either `true` or `false`
  return hit;
};

```
<a id='casestudy'></a>
Case study: Treasure Hunter
---------------

So I told you that you now have all the skills you need to start
making games. What? You don't believe me? Let me prove it to you! Let’s take a
close at how to make a simple object collection and enemy
avoidance game called **Treasure Hunter**. (You'll find it the `examples`
folder.)

![Treasure Hunter](/examples/images/screenshots/26.png)

Treasure Hunter is a good example of one of simplest complete
games you can make using the tools you've learnt so far. Use the
keyboard arrow
keys to help the explorer find the treasure and carry it to the exit.
Six blob monsters move up and down between the dungeon walls, and if
they hit the explorer he becomes semi-transparent and the health meter
at the top right corner shrinks. If all the health is used up, “You
Lost!” is displayed on the stage; if the explorer reaches the exit with
the treasure, “You Won!” is displayed. Although it’s a basic
prototype, Treasure Hunter contains most of the elements you’ll find
in much bigger games: texture atlas graphics, interactivity,
collision, and multiple game scenes. Let’s go on a tour of how the
game was put together so that you can use it as a starting point for one of your own games.

### The code structure

Open the `treasureHunter.html` file and you'll see that all the game
code is in one big file. Here's a birds-eye view of how all the code is
organized.

```js
//Setup Pixi and load the texture atlas files - call the `setup`
//function when they've loaded

function setup() {
  //Initialize the game sprites, set the game `state` to `play`
  //and start the 'gameLoop'
}

function gameLoop() {
  //Runs the current game `state` in a loop and renders the sprites
}

function play() {
  //All the game logic goes here
}

function end() {
  //All the code that should run at the end of the game
}

//The game's helper functions:
//`keyboard`, `hitTestRectangle`, `contain` and `randomInt`
```
Use this as your world map to the game as we look at how each
section works.

<a id='initialize'></a>
### Initialize the game in the setup function

As soon as the texture atlas images have loaded, the `setup` function
runs. It only runs once, and lets you perform
one-time setup tasks for your game. It's a great place to create and initialize
objects, sprites, game scenes, populate data arrays or parse
loaded JSON game data.

Here's an abridged view of the `setup` function in Treasure Hunter,
and the tasks that it performs.

```js
function setup() {
  //Create the `gameScene` group
  //Create the `door` sprite
  //Create the `player` sprite
  //Create the `treasure` sprite
  //Make the enemies
  //Create the health bar
  //Add some text for the game over message
  //Create a `gameOverScene` group
  //Assign the player's keyboard controllers

  //set the game state to `play`
  state = play;

  //Start the game loop
  gameLoop();
}

```
The last two lines of code, `state = play;` and `gameLoop()` are perhaps
the most important. Running `gameLoop` switches on the game's engine,
and causes the `play` function to be called in a continuous loop. But before we look at how that works, let's see what the
specific code inside the `setup` function does.

<a id='gamescene'></a>
####Creating the game scenes

The `setup` function creates two `Container` groups called
`gameScene` and `gameOverScene`. Each of these are added to the stage.
```js
gameScene = new Container();
stage.addChild(gameScene);

gameOverScene = new Container();
stage.addChild(gameOverScene);

```
All of the sprites that are part of the main game are added to the
`gameScene` group. The game over text that should be displayed at the
end of the game is added to the `gameOverScene` group.

![Displaying text](/examples/images/screenshots/27.png)

Although it's created in the `setup` function, the `gameOverScene`
shouldn't be visible when the game first starts, so its `visible`
property is initialized to `false`.
```js
gameOverScene.visible = false;
```
You'll see ahead that, when the game ends, the `gameOverScene`'s `visible`
property will be set to `true` to display the text that appears at the
end of the game.

<a id='makingdungon'></a>
####Making the dungeon, door, explorer and treasure

The player, exit door, treasure chest and the dungeon background image
are all sprites made from texture atlas frames. Very importantly,
they're all added as children of the `gameScene`.
```js
//Create an alias for the texture atlas frame ids
id = resources["images/treasureHunter.json"].textures;

//Dungeon
dungeon = new Sprite(id["dungeon.png"]);
gameScene.addChild(dungeon);

//Door
door = new Sprite(id["door.png"]);
door.position.set(32, 0);
gameScene.addChild(door);

//Explorer
explorer = new Sprite(id["explorer.png"]);
explorer.x = 68;
explorer.y = gameScene.height / 2 - explorer.height / 2;
explorer.vx = 0;
explorer.vy = 0;
gameScene.addChild(explorer);

//Treasure
treasure = new Sprite(id["treasure.png"]);
treasure.x = gameScene.width - treasure.width - 48;
treasure.y = gameScene.height / 2 - treasure.height / 2;
gameScene.addChild(treasure);
```
Keeping them together in the `gameScene` group will make it easy for
us to hide the `gameScene` and display the `gameOverScene` when the game is finished.

<a id='makingblob'></a>
####Making the blob monsters

The six blob monsters are created in a loop. Each blob is given a
random initial position and velocity. The vertical velocity is
alternately multiplied by `1` or `-1` for each blob, and that’s what
causes each blob to move in the opposite direction to the one next to
it. Each blob monster that's created is pushed into an array called
`blobs`.
```js
var numberOfBlobs = 6,
    spacing = 48,
    xOffset = 150,
    speed = 2,
    direction = 1;

//An array to store all the blob monsters
blobs = [];

//Make as many blobs as there are `numberOfBlobs`
for (var i = 0; i < numberOfBlobs; i++) {

  //Make a blob
  var blob = new Sprite(id["blob.png"]);

  //Space each blob horizontally according to the `spacing` value.
  //`xOffset` determines the point from the left of the screen
  //at which the first blob should be added
  var x = spacing * i + xOffset;

  //Give the blob a random `y` position
  var y = randomInt(0, stage.height - blob.height);

  //Set the blob's position
  blob.x = x;
  blob.y = y;

  //Set the blob's vertical velocity. `direction` will be either `1` or
  //`-1`. `1` means the enemy will move down and `-1` means the blob will
  //move up. Multiplying `direction` by `speed` determines the blob's
  //vertical direction
  blob.vy = speed * direction;

  //Reverse the direction for the next blob
  direction *= -1;

  //Push the blob into the `blobs` array
  blobs.push(blob);

  //Add the blob to the `gameScene`
  gameScene.addChild(blob);
}

```
<a id='healthbar'></a>
####Making the health bar

When you play Treasure Hunter you'll notice that when the explorer touches
one of the enemies, the width of the health bar at the top right
corner of the screen decreases. How was this health bar made? It's
just two overlapping rectangles at exactly the same position: a black rectangle behind, and
a red rectangle in front. They're grouped into a single `healthBar`
group. The `healthBar` is then added to the `gameScene` and positioned
on the stage.
```js
//Create the health bar
healthBar = new PIXI.DisplayObjectContainer();
healthBar.position.set(stage.width - 170, 6)
gameScene.addChild(healthBar);

//Create the black background rectangle
var innerBar = new PIXI.Graphics();
innerBar.beginFill(0x000000);
innerBar.drawRect(0, 0, 128, 8);
innerBar.endFill();
healthBar.addChild(innerBar);

//Create the front red rectangle
var outerBar = new PIXI.Graphics();
outerBar.beginFill(0xFF3300);
outerBar.drawRect(0, 0, 128, 8);
outerBar.endFill();
healthBar.addChild(outerBar);

healthBar.outer = outerBar;
```
You can see that a property called `outer` has been added to the
`healthBar`. It just references the `outerBar` (the red rectangle) so that it will be convenient to access later.
```js
healthBar.outer = outerBar;
```
You don't have to do this; but, hey why not! It means that if you want
to control the width of the red `outerBar`, you can write some smooth code that looks like this:
```js
healthBar.outer.width = 30;
```
That's pretty neat and readable, so we'll keep it!

<a id='message'></a>
####Making the message text

When the game is finished, some text displays “You won!” or “You
lost!”, depending on the outcome of the game. This is made using a
text sprite and adding it to the `gameOverScene`. Because the
`gameOverScene`‘s `visible` property is set to `false` when the game
starts, you can’t see this text. Here’s the code from the `setup`
function that creates the message text and adds it to the
`gameOverScene`.
```js
message = new Text(
  "The End!",
  {font: "64px Futura", fill: "white"}
);

message.x = 120;
message.y = stage.height / 2 - 32;

gameOverScene.addChild(message);
```
<a id='playing'></a>
###Playing the game

All the game logic and the code that makes the sprites move happens
inside the `play` function, which runs in a continuous loop. Here's an
overview of what the `play` function does
```js
function play() {
  //Move the explorer and contain it inside the dungeon
  //Move the blob monsters
  //Check for a collision between the blobs and the explorer
  //Check for a collision between the explorer and the treasure
  //Check for a collsion between the treasure and the door
  //Decide whether the game has been won or lost
  //Change the game `state` to `end` when the game is finsihed
}
```
Let's find out how all these features work.

<a id='movingexplorer'></a>
###Moving the explorer

The explorer is controlled using the keyboard, and the code that does
that is very similar to the keyboard control code you learnt earlier.
The `keyboard` objects modify the explorer’s velocity, and that
velocity is added to the explorer’s position inside the `play`
function.
```js
explorer.x += explorer.vx;
explorer.y += explorer.vy;
```
<a id='containingmovement'></a>
####Containing movement

But what's new is that the explorer's movement is contained inside the walls of the
dungeon. The green outline shows the limits of the explorer's
movement.

![Displaying text](/examples/images/screenshots/28.png)

That's done with the help of a custom function called
`contain`.
```js
contain(explorer, {x: 28, y: 10, width: 488, height: 480});
```
`contain` takes two arguments. The first is the sprite you want to keep
contained. The second is any object with `x`, `y`, `width` and
`height` properties that define a rectangular area. In this example,
the containing object defines an area that's just slightly offset
from, and smaller than, the stage. It matches dimensions of the dungeon
walls.

Here's the `contain` function that does all this work. The function checks
to see if the sprite has crossed the boundaries of the containing
object. If it has, the code moves the sprite back into that boundary.
The `contain` function also returns a `collision` variable with the
value "top", "right", "bottom" or "left", depending on which side of
the boundary the sprite hit. (`collision` will be `undefined` if the
sprite didn't hit any of the boundaries.)
```js
function contain(sprite, container) {

  var collision = undefined;

  //Left
  if (sprite.x < container.x) {
    sprite.x = container.x;
    collision = "left";
  }

  //Top
  if (sprite.y < container.y) {
    sprite.y = container.y;
    collision = "top";
  }

  //Right
  if (sprite.x + sprite.width > container.width) {
    sprite.x = container.width - sprite.width;
    collision = "right";
  }

  //Bottom
  if (sprite.y + sprite.height > container.height) {
    sprite.y = container.height - sprite.height;
    collision = "bottom";
  }

  //Return the `collision` value
  return collision;
}
```
You'll see how the `collision` return value will be use in the code
ahead to make the blob monsters bounce back and forth between the top
and bottom dungeon walls.

<a id='movingmonsters'></a>
###Moving the monsters

The `play` function also moves the blob monsters, keeps them contained
inside the dungeon walls, and checks each one for a collision with the
player. If a blob bumps into the dungeon’s top or bottom walls, its
direction is reversed. All this is done with the help of a `forEach` loop
which iterates through each of `blob` sprites in the `blobs` array on
every frame.
```js
blobs.forEach(function(blob) {

  //Move the blob
  blob.y += blob.vy;

  //Check the blob's screen boundaries
  var blobHitsWall = contain(blob, {x: 28, y: 10, width: 488, height: 480});

  //If the blob hits the top or bottom of the stage, reverse
  //its direction
  if (blobHitsWall === "top" || blobHitsWall === "bottom") {
    blob.vy *= -1;
  }

  //Test for a collision. If any of the enemies are touching
  //the explorer, set `explorerHit` to `true`
  if(hitTestRectangle(explorer, blob)) {
    explorerHit = true;
  }
});

```
You can see in this code above how the return value of the `contain`
function is used to make the blobs bounce off the walls. A variable
called `blobHitsWall` is used to capture the return value:
```js
var blobHitsWall = contain(blob, {x: 28, y: 10, width: 488, height: 480});
```
`blobHitsWall` will usually be `undefined`. But if the blob hits the
top wall, `blobHitsWall` will have the value "top". If the blob hits
the bottom wall, `blobHitsWall` will have the value "bottom". If
either of these cases are `true`, you can reverse the blob's direction
by reversing its velocity. Here's the code that does this:
```js
if (blobHitsWall === "top" || blobHitsWall === "bottom") {
  blob.vy *= -1;
}
```
Multiplying the blob's `vy` (vertical velocity) value by `-1` will flip
the direction of its movement.

<a id='checkingcollisions'></a>
###Checking for collisions

The code in the loop above uses `hitTestRectangle` to figure
out if any of the enemies have touched the explorer.
```js
if(hitTestRectangle(explorer, blob)) {
  explorerHit = true;
}
```
If `hitTestRectangle` returns `true`, it means there’s been a collision
and a variable called `explorerHit` is set to `true`. If `explorerHit`
is `true`, the `play` function makes the explorer semi-transparent
and reduces the width of the `health` bar by 1 pixel.
```js
if(explorerHit) {

  //Make the explorer semi-transparent
  explorer.alpha = 0.5;

  //Reduce the width of the health bar's inner rectangle by 1 pixel
  healthBar.outer.width -= 1;

} else {

  //Make the explorer fully opaque (non-transparent) if it hasn't been hit
  explorer.alpha = 1;
}

```
If  `explorerHit` is `false`, the explorer's `alpha` property is
maintained at 1, which makes it fully opaque.

The `play` function also checks for a collision between the treasure
chest and the explorer. If there’s a hit, the `treasure` is set to the
explorer’s position, with a slight offset. This makes it look like the
explorer is carrying the treasure.

![Displaying text](/examples/images/screenshots/29.png)

Here's the code that does this:

```js
if (hitTestRectangle(explorer, treasure)) {
  treasure.x = explorer.x + 8;
  treasure.y = explorer.y + 8;
}
```
<a id='reachingexit'></a>
###Reaching the exit door and ending the game

There are two ways the game can end: You can win if you carry the
treasure to the exit, or you can lose if you run out of health.

To win the game, the treasure chest just needs to touch the exit door. If
that happens, the game `state` is set to `end`, and the `message` text
displays "You won".
```js
if (hitTestRectangle(treasure, door)) {
  state = end;
  message.text = "You won!";
}
```
If you run out of health, you lose the game. The game `state` is also
set to `end` and the `message` text displays "You Lost!"
```js
if (healthBar.outer.width < 0) {
  state = end;
  message.text = "You lost!";
}
```
But what does this mean?
```js
state = end;
```
You'll remember from earlier examples that the `gameLoop` is constantly updating a function called
`state` at 60 times per second. Here's the `gameLoop`that does this:
```js
function gameLoop(){

  //Loop this function 60 times per second
  requestAnimationFrame(gameLoop);

  //Update the current game state
  state();

  //Render the stage
  renderer.render(stage);
}
```
You'll also remember that we initially set the value of
`state` to `play`, which is why the `play` function runs in a loop.
By setting `state` to `end` we're telling the code that we want
another function, called `end` to run in a loop. In a bigger game you
could have a `tileScene` state, and states for each game level, like
`leveOne`, `levelTwo` and `levelThree`.

So what is that `end` function? Here it is!
```js
function end() {
  gameScene.visible = false;
  gameOverScene.visible = true;
}
```
It just flips the visibility of the game scenes. This is what hides
the `gameScene` and displays the `gameOverScene` when the game ends.

This is a really simple example of how to switch a game's state, but
you can have as many game states as you like in your games, and fill them
with as much code as you need. Just change the value of `state` to
whatever function you want to run in a loop.

And that’s really all there is to Treasure Hunter! With a little more work you could turn this simple prototype into a full game – try it!

<a id='spriteproperties'></a>
More about sprites
-----------------------------

You've learnt how to use quite a few useful sprite properties so far, like `x`, `y`,
`visible`, and `rotation` that give you a lot of control over a
sprite's position and appearance. But Pixi Sprites also have many more
useful properties that are fun to play with. [Here's the full list.](http://pixijs.github.io/docs/PIXI.Sprite.html)

How does Pixi’s class inheritance system work? ([What is a **class**
and what is **inheritence**? Click this link to find out.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)) Pixi’s sprites are
built on an inheritance model that follows this chain:
```
DisplayObject > Container > Sprite
```
Inheritance just means that the classes later in the chain use
properties and methods from classes earlier in the chain.
The most basic class is `DisplayObject`. Anything that’s a
`DisplayObject` can be rendered on the stage. `Container`
is the next class in the inheritance chain. It allows `DisplayObject`s
to act as containers for other `DisplayObject`s. Third up the chain is
the `Sprite` class. That’s the class you’ll be using to make most of
your game objects. However, later you’ll learn how to use
`Container`s to group sprites together.

<a id='takingitfurther'></a>
Taking it further
-----------------

Pixi can do a lot, but it can't do everything! If you want to start
making games or complex interactive applications with Pixi, you'll need
to use some helper libraries:

- [Bump](https://github.com/kittykatattack/bump): A complete suite of 2D collision functions for games.
- [Tink](https://github.com/kittykatattack/tink): Drag-and-drop, buttons, a universal pointer and other
  helpful interactivity tools.
- [Charm](https://github.com/kittykatattack/charm): Easy-to-use tweening animation effects for Pixi sprites.
- [Dust](https://github.com/kittykatattack/dust): Particle effects for creating things like explosions, fire
  and magic.
- [Sprite Utilities](https://github.com/kittykatattack/spriteUtilities): Easier and more intuitive ways to
  create and use Pixi sprites, as well adding a state machine and
  animation player. Makes working with Pixi a lot more fun.
- [Sound.js](https://github.com/kittykatattack/sound.js): A micro-library for loading, controlling and generating
  sound and music effects. Everything you need to add sound to games.
- [Smoothie](https://github.com/kittykatattack/smoothie): Ultra-smooth sprite animation using true delta-time interpolation. It also lets you specify the fps (frames-per-second) at which your game or application runs, and completely separates your sprite rendering loop from your application logic loop.

You can find out how to use all these libraries with Pixi in the book 
[Learn PixiJS](http://www.springer.com/us/book/9781484210956).

<a id='hexi'></a>
###Hexi

Do you want to use all the functionality of those libraries, but don't
want the hassle of integrating them yourself? Use **Hexi**: a complete
development environment for building games and interactive
applications:

https://github.com/kittykatattack/hexi

It bundles the best version of Pixi (the latest stable one) with all these 
libraries (and more!) for a simple and fun way to make games. Hexi also
lets you access the global `PIXI` object directly, so you can write
low-level Pixi code directly in a Hexi application, and optionally choose to use as many or
as few of Hexi's extra conveniences as you need.

<a id='supportingthisproject'></a>
Please help to support this project!
-------------------

Buy the book! Incredibly, someone actually paid me to finish writing this tutorial
and turn it into a book! 

[Learn PixiJS](http://www.springer.com/us/book/9781484210956)

(And it's not just some junky "e-book", but a real, heavy, paper book, published by Springer,
the world's largest publisher! That means you can invite your friends
over, set it on fire, and roast marshmallows!!) There's 80% more
content than what's in this tutorial, and it's
packed full of all the essential techniques you need to know to use
Pixi to make all kinds of interactive applications and games.

Find out how to:

- Make animated game characters.
- Create a full-featured animation state player.
- Dynamically animate lines and shapes.
- Use tiling sprites for infinite parallax scrolling.
- Use blend modes, filters, tinting, masks, video, and render textures.
- Produce content for multiple resolutions.
- Create interactive buttons.
- Create a flexible drag and drop interface for Pixi.
- Create particle effects.
- Build a stable software architectural model that will scale to any size.
- Make complete games.

And, as a bonus, all the code is written entirely in the latest version of
JavaScript: ES6/2015.

If you want to support this project, please buy a copy of this book,
and buy another copy for your mom!

