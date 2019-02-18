# html

## 1.对html5的了解

- 语义标签

  | 标签                  | 描述                             |
  | --------------------- | -------------------------------- |
  | <header></header>     | 定义了文档的头部区域             |
  | <footer></footer>     | 定义了文档的尾部区域             |
  | <nav></nav>           | 定义文档的导航                   |
  | <section></section>   | 定义文档中的节（section、区段）  |
  | <article></article>   | 定义页面独立的内容区域           |
  | <aside></aside>       | 定义页面的侧边栏内容             |
  | <detailes></detailes> | 用于描述文档或文档某个部分的细节 |
  | <summary></summary>   | 标签包含 details 元素的标题      |
  | <dialog></dialog>     | 定义对话框，比如提示框           |

- 增强型表单，HTML5 拥有多个新的表单 Input 输入类型。这些新特性提供了更好的输入控制和验证。

  | 输入类型       | 描述                         |
  | -------------- | ---------------------------- |
  | color          | 主要用于选取颜色             |
  | date           | 从一个日期选择器选择一个日期 |
  | datetime       | 选择一个日期（UTC 时间）     |
  | datetime-local | 选择一个日期和时间 (无时区)  |
  | email          | 包含 e-mail 地址的输入域     |
  | month          | 选择一个月份                 |
  | number         | 数值的输入域                 |
  | range          | 一定范围内数字值的输入域     |
  | search         | 用于搜索域                   |
  | tel            | 定义输入电话号码字段         |
  | time           | 选择一个时间                 |
  | url            | URL 地址的输入域             |
  | week           | 选择周和年                   |

   HTML5 也新增以下表单元素

  | 表单元素   | 描述                                                         |
  | ---------- | ------------------------------------------------------------ |
  | <datalist> | 元素规定输入域的选项列表使用 <input> 元素的 list 属性与 <datalist> 元素的 id 绑定 |
  | <keygen>   | 提供一种验证用户的可靠方法标签规定用于表单的密钥对生成器字段。 |
  | <output>   | 用于不同类型的输出比如计算或脚本输出                         |

  HTML5 新增的表单属性

  - placehoder 属性，简短的提示在用户输入值前会显示在输入域上。即我们常见的输入框默认提示，在用户输入后消失。

  - required  属性，是一个 boolean 属性。要求填写的输入域不能为空
  - pattern 属性，描述了一个正则表达式用于验证<input> 元素的值。
  - min 和 max 属性，设置元素最小值与最大值。
  - step 属性，为输入域规定合法的数字间隔。
  - height 和 width 属性，用于 image 类型的 <input> 标签的图像高度和宽度。
  - autofocus 属性，是一个 boolean 属性。规定在页面加载时，域自动地获得焦点。
  - multiple 属性 ，是一个 boolean 属性。规定<input> 元素中可选择多个值。

- 视频和音频

  - HTML5 提供了播放音频文件的标准，即使用 <audio> 元素

    ```
    <audio controls>
      <source src="horse.ogg" type="audio/ogg">
      <source src="horse.mp3" type="audio/mpeg">
    您的浏览器不支持 audio 元素。
    </audio>
    ```

  　control 属性供添加播放、暂停和音量控件。

  　在<audio> 与 </audio> 之间你需要插入浏览器不支持的<audio>元素的提示文本 。<audio> 元素允许使用多个 <source> 元素. <source> 元素可以链接不同的音频文件，浏览器将使用第一个支持的音频文件


  　目前, <audio>元素支持三种音频格式文件: MP3, Wav, 和 Ogg

  - HTML5 规定了一种通过 video 元素来包含视频的标准方法。

    ```
    <video width="320" height="240" controls>
      <source src="movie.mp4" type="video/mp4">
      <source src="movie.ogg" type="video/ogg">
    您的浏览器不支持Video标签。
    </video>
    ```

    control 提供了 播放、暂停和音量控件来控制视频。也可以使用dom操作来控制视频的播放暂停，如 play() 和 pause() 方法。

    同时 video 元素也提供了 width 和 height 属性控制视频的尺寸.如果设置的高度和宽度，所需的视频空间会在页面加载时保留。如果没有设置这些属性，浏览器不知道大小的视频，浏览器就不能再加载时保留特定的空间，页面就会根据原始视频的大小而改变。

    与 标签之间插入的内容是提供给不支持 video 元素的浏览器显示的。

    video 元素支持多个source 元素. 元素可以链接不同的视频文件。浏览器将使用第一个可识别的格式（ MP4, WebM, 和 Ogg）

- Canvas绘图

  - 创建一个画布，一个画布在网页中是一个矩形框，通过 <canvas> 元素来绘制。默认情况下 元素没有边框和内容。

    ```
    <canvas id="myCanvas" width="200" height="100" style="border:1px solid #000000;"></canvas>
    ```

    标签通常需要指定一个id属性 (脚本中经常引用), width 和 height 属性定义的画布的大小，使用 style 属性来添加边框。你可以在HTML页面中使用多个 <canvas> 元素

  - 使用Javascript来绘制图像，canvas 元素本身是没有绘图能力的。所有的绘制工作必须在 JavaScript 内部完成

    ```
    <script>
    　　var c=document.getElementById("myCanvas");
    　　var ctx=c.getContext("2d");
    　　ctx.fillStyle="#FF0000";
    　　ctx.fillRect(0,0,150,75);
    </script>
    ```

    getContext("2d") 对象是内建的 HTML5 对象，拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。

    设置 fillStyle 属性可以是CSS颜色，渐变，或图案。fillStyle默认设置是#000000（黑色）。fillRect(x,y,width,height) 方法定义了矩形当前的填充方式。意思是：在画布上绘制 150x75 的矩形，从左上角开始 (0,0)。　

- SVG是指可伸缩的矢量图形

  SVG 与 Canvas两者间的区别

  - SVG 是一种使用 XML 描述 2D 图形的语言。

  - Canvas 通过 JavaScript 来绘制 2D 图形。

  - SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript 事件处理器。

  - 在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

  - Canvas 是逐像素进行渲染的。在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

- 地理定位

  HTML5 Geolocation（地理定位）用于定位用户的位置。

  ```
  window.navigator.geolocation {
      getCurrentPosition:  fn  用于获取当前的位置数据
      watchPosition: fn  监视用户位置的改变
      clearWatch: fn  清除定位监视
  }　
  ```

  获取用户定位信息：

  ```
  navigator.geolocation.getCurrentPosition(
      function(pos){
  　　　　console.log('用户定位数据获取成功')
  　　　　//console.log(arguments);
  　　　　console.log('定位时间：',pos.timestamp)
  　　　　console.log('经度：',pos.coords.longitude)
  　　　　console.log('纬度：',pos.coords.latitude)
  　　　　console.log('海拔：',pos.coords.altitude)
  　　　　console.log('速度：',pos.coords.speed)
  	},    //定位成功的回调
  	function(err){ 
  　　　　console.log('用户定位数据获取失败')
  　　　　//console.log(arguments);
  	}        //定位失败的回调
  )
  ```

- 拖放API

  - 拖放是一种常见的特性，即抓取对象以后拖到另一个位置。在 HTML5 中，拖放是标准的一部分，任何元素都能够拖放。

  - 拖放的过程分为源对象和目标对象。源对象是指你即将拖动元素，而目标对象则是指拖动之后要放置的目标位置。

  - 拖放的源对象(可能发生移动)可以触发的事件——3个

    dragstart：拖动开始

    drag：拖动中

    dragend：拖动结束

    整个拖动过程的组成： dragstart*1 + drag*n + dragend*1

  - 拖放的目标对象(不会发生移动)可以触发的事件——4个：

  ​	dragenter：拖动着进入

  ​	dragover：拖动着悬停

  ​	dragleave：拖动着离开

  ​	drop：释放

  ​	整个拖动过程的组成1： dragenter*1 + dragover*n + dragleave*1

  ​	整个拖动过程的组成2： dragenter*1 + dragover*n + drop*1

  - dataTransfer：用于数据传递的“拖拉机”对象；

      在拖动源对象事件中使用e.dataTransfer属性保存数据：

    e.dataTransfer.setData( k,  v )

      在拖动目标对象事件中使用e.dataTransfer属性读取数据：

    var value = e.dataTransfer.getData( k )

- Web Worker

  当在 HTML 页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。

  web worker 是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行。

- Web Storage

  使用HTML5可以在本地存储用户的浏览数据。早些时候,本地存储使用的是cookies。但是Web 存储需要更加的安全与快速. 这些数据不会被保存在服务器上，但是这些数据只用于用户请求网站数据上.它也可以存储大量的数据，而不影响网站的性能。数据以 键/值 对存在, web网页的数据只允许该网页访问使用。

  客户端存储数据的两个对象为：

  - localStorage - 没有时间限制的数据存储
  - sessionStorage - 针对一个 session 的数据存储, 当用户关闭浏览器窗口后，数据会被删除。

  不管是 localStorage，还是 sessionStorage，可使用的API都相同，常用的有如下几个（以localStorage为例）：

  - 保存数据：localStorage.setItem(key,value);
  - 读取数据：localStorage.getItem(key);
  - 删除单个数据：localStorage.removeItem(key);
  - 删除所有数据：localStorage.clear();
  - 得到某个索引的key：localStorage.key(index);

- WebSocket

  WebSocket是HTML5开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。在WebSocket API中，浏览器和服务器只需要做一个握手的动作，然后，浏览器和服务器之间就形成了一条快速通道。两者之间就直接可以数据互相传送。浏览器通过 JavaScript 向服务器发出建立 WebSocket 连接的请求，连接建立以后，客户端和服务器端就可以通过 TCP 连接直接交换数据。当你获取 Web Socket 连接后，你可以通过 **send()** 方法来向服务器发送数据，并通过 **onmessage** 事件来接收服务器返回的数据。

### 详情请参考:

http://www.cnblogs.com/vicky1018/p/7705223.html