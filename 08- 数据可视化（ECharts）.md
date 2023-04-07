# 08- 数据可视化	(ECharts)

# 一、基础篇

## 1. **数据可视化前言**

### 1.1 **什么是数据可视化**

数据可视化, 说白了, 就是把数据以更加直观的方式进行呈现. 那什么方式是更加直观的方式呢? 就是**图表**

常言道, 文不如表, 表不如图, 人们大脑对图的敏感程度要比苍白无力的文字好很多.

我们来看一组数据.

``` txt
衬衫:5 
羊毛衫:20 
雪纺衫:36 
裤子:10 
高跟鞋:10 
袜子:20
```

这个数据就是某些产品的销量. 单纯从这些文字上来看, 很难看出数据之间对比的关系. 如果把这些数据以图表的方式呈现出来呢 ?

这个数据就是某些产品的销量. 单纯从这些文字上来看, 很难看出数据之间对比的关系. 如果把这些数据以图表的方式呈现出来呢 ?

![image-20220822085827055](.\assets\image-20220822085827055.png)

上面这幅图就是这组数据的图表展示. 通过这幅图一眼就能看出哪些产品销量高, 哪些产品销量低. 数据与数据之间的关系一目了然.

### **1.2.** 数据可视化的好处

+ 清晰有效地传达与沟通信息

数据可视化的好处之一就是能够清晰有效的传达信息和沟通信息. 继续看刚才的那个例子, 如果使用同样的数据, 换成另外一种展现形式, 比如下边的这幅饼图. 我们可以很容易的就看出每个产品的销量占比.不需要太多的脑力计算和思维转换. 

![image-20220822090042723](.\assets\image-20220822090042723.png)

+ 更容易洞察隐藏在数据中的信息

将数据以图表的方式呈现出来还可以帮助我们感受到那些隐藏在数据之间的信息.比如下面的这幅上证指数的k线图

![image-20220822090113772](.\assets\image-20220822090113772.png)

这幅图中可以看出指数的上升趋势或者下降趋势. 而上升趋势或者下降趋势这种信息是很难从文字中察觉到



### 1.3 **数据可视化的实现方式**

+ 报表类

  + Excel
  + 水晶报表

  > 报表类的主要实现方式就大家熟悉的Excel或者水晶报表, 这种方式主要面向的是非技术人员, 在特定 
  >
  > 的软件中点击几个按钮,添加一些数据就可以生成图标了.这种方式的优点是简单, 谁都会用. 缺点也显 
  >
  > 而易见, 就是不灵活, 图表一旦生成之后就固定不变了, 如果数据发生变化了, 图表需要重新生成

+ 商业智能 **BI**

  + 微软BI
  + Power BI

  > 商业智能BI的实现方式主要有微软的BI和Power-BI, 它比报表类更加高端, 他除了可以对数据生成报 
  >
  > 表之外, 还可以提出决策依据，帮助企业做出明智的业务经营决策 

+ 编码类

  + ECharts
  + D3.js

  > 编码类, 这种是需要程序员参与, 程序员可以对接到公司现有的系统架构中进行编码, 实时生成动态的 
  >
  > 图表.常见的使用库有ECharts.js和D3.js, 我们项目中使用的是ECharts.js , 他是百度公司开发 
  >
  > 的一套开源可视化库, D3.js是国外的一个可视化库, 在封装性\易用性\效果上, ECharts要更优秀 
  >
  > 一些.

相对来说,这三种方式中编码类的实现方式更加灵活, 他可以融入到我们已有的项目中,和项目的贴合度是最高的, 但是他的门槛也高些, 需要有编程基础才能完成. 而我们的这么课程正是编码类可视化的实现, 并且选择的是百度开源的 `ECharts.js`



## 2. `ECharts`**的基本使用**

### 2.1 `ECharts`**的介绍**

ECharts是百度公司开源的一个使用 JavaScript 实现的开源可视化库，兼容性强，底层依赖矢量图形库 ZRender ，提供直观，交互丰富，可高度个性化定制的数据可视化图表。

+ 开源免费
+ 功能丰富
+ 社区活跃
+ 多种数据支持
+ 移动端优化
+ 跨平台

> ECharts 能够做出各种各样漂亮的图表，它能满足绝大多数可视化图表的实现.它的兼容性强, 使用方便, 
>
> 功能强大, 是实现数据可视化的最佳选择之一, 更多特点和介绍可以查阅官网地址： 
>
> https://echarts.apache.org/zh/index.html 



### 2.2 `ECharts`**的快速上手**

`ECharts `的入门使用特别简单, 5分钟就能够上手. 他大体分为这几个步骤

+ 步骤1：引入 echarts.js 文件

  echarts是一个 js 的库，当然得先引入这个库文件

  ``` js
  <script src="js/echarts.min.js"></script>
  ```

+ 步骤2：准备一个呈现图表的盒子

  这个盒子通常来说就是我们熟悉的 div ，这个 div 决定了图表显示在哪里

  ``` html
  <div id="main" style="width: 600px;height:400px;"></div>
  ```

+ 步骤3：初始化 echarts 实例对象

  在这个步骤中, 需要指明图表最终显示在哪里的DOM元素

  ``` js
  var myChart = echarts.init(document.getElementById('main'))
  ```

+ 步骤4：准备配置项

  这步很关键，我们最终的效果，到底是显示饼图还是折线图，基本上都是由配置项决定的

  ``` js
  var option = { 
      xAxis: { type: 'category', data: ['小明', '小红', '小王'] },
      yAxis: { type: 'value' },
      series: [ { name: '语文', type: 'bar', data: [70, 92, 87], } ] 
  }
  ```

+ 步骤5：将配置项设置给 echarts 实例对象

  ``` js
  myChart.setOption(option)
  ```

通过简单的5个步骤, 就能够把一个简单的柱状图给显示在网页中了.这几个步骤中, 步骤4最重要,一个图表最终呈现什么样子,完全取决于这个配置项.所以对于不同的图表, 除了配置项会发生改变之外,其他的代码 都是固定不变的.



### 2.3 **相关配置讲解**

+ `xAxis`

  直角坐标系 中的 x 轴, 如果 type 属性的值为 category ,那么需要配置 data 数据, 代表在 x 轴的呈现

+ `yAxis`

  直角坐标系 中的 y 轴, 如果 type 属性配置为 value , 那么无需配置 data , 此时 y 轴会自动去series 下找数据进行图表的绘制

+ `series`

  系列列表。每个系列通过 type 决定自己的图表类型, data 来设置每个系列的数据

配置项都是以**键值对**的形式存在, 并且配置项有很多,` ECharts `的学习大多是针对于这些配置项的, 对于配置项的学习, 大家可以不用死记硬背, 需要的时候查一查官方文档即可. 

网址: https://echarts.apache.org/zh/option.html , 常用的配置项多用几次, 你自然而然就记下了

同学们可以查文档试一下: title中的各种配置

``` js
title: { show: true, text: '标题', link: 'http://www.baidu.cn', textStyle: { color: 'red' } }
```



## 3. ECharts**常用图表**

### 3.1 **图表1  柱状图**

#### 3.1.1 **柱状图的实现步骤**

+ 步骤1 ECharts 最基本的代码结构

  ``` html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head>
          <script src="js/echarts.min.js"></script>
      </head> 
      <body>
          <div style="width: 600px;height:400px"></div> 
          <script>
              var mCharts = echarts.init(document.querySelector("div")) 
              var option = {}
              mCharts.setOption(option) 
          </script> 
      </body> 
  </html>
  ```

+ 步骤2 准备x轴的数据

  ``` js
  var xDataArr = ['张三', '李四', '王五', '闰土', '小明', '茅台', '二妞', '大强']
  ```

+ 步骤3 准备 y 轴的数据

  ``` js
  var yDataArr = [88, 92, 63, 77, 94, 80, 72, 86]
  ```

+ 步骤4 准备 option , 将 series 中的 type 的值设置为: bar 

  ``` js
  var option = { 
      xAxis: { type: 'category', data: xDataArr },
      yAxis: { type: 'value' },
      series: [ { type: 'bar', data: yDataArr } ] 
  }
  ```

  **注意: **

  **坐标轴 xAxis 或者 yAxis 中的配置, type 的值主要有两种: category 和 value **

  **如果 type属性的值为 category ,那么需要配置 data 数据, 代表在 x 轴的呈现. **

  **如果 type 属性配置为 value ,那么无需配置 data , 此时 y 轴会自动去 series 下找数据进行图表的绘制**

最终的效果如下图:

![image-20220822091702339](.\assets\image-20220822091702339.png)

#### 3.1.2 **柱状图的常见效果**

+ 标记:

  + 最大值\最小值 `markPoint`

    ``` js
    series: [ { 
        ...... 
        markPoint: { data: [ 
            { type: 'max', name: '最大值' },{ type: 'min', name: '最小值' } 
        ] }
    } ]
    ```

    ![image-20220822091832447](.\assets\image-20220822091832447.png)

  + 平均值 `markLine`

    ``` js
    series: [ { ...... markLine: { data: [ { type: 'average', name: '平均值' } ] } } ]
    ```

     ![image-20220822091917935](.\assets\image-20220822091917935.png)

+ 显示

  + 数值显示` label`

    ``` js
    series: [ { ...... label: { show: true, // 是否可见 rotate: 60 // 旋转角度 } } ]
    ```

    ![image-20220822092009548](.\assets\image-20220822092009548.png)

  + 柱宽度 `barWidth `

    ``` js
    series: [ { ...... barWidth: '30%' // 柱的宽度 } ]
    ```

    ![image-20220822092051818](.\assets\image-20220822092051818.png)

  + 横向柱状图

    所谓的横向柱状图, 只需要让x轴的角色和y轴的角色互换一下即可. 既 `xAxis` 的` type` 设置为

    `value` , `yAxis` 的 `type` 设置为 `category `, 并且设置 `data` 即可

    ``` js
    var option = { 
        xAxis: { type: 'value' },
        yAxis: { type: 'category', data: xDataArr },
        series: [ { type: 'bar', data: yDataArr } ] 
    }
    ```

    ![image-20220822092214455](.\assets\image-20220822092214455.png)

#### 3.1.3 **柱状图特点**

柱状图描述的是分类数据，呈现的是每一个分类中『有多少？』, 图表所表达出来的含义在于不同类别数据的排名\对比情况



#### 3.1.4.通用配置

使用` ECharts` 绘制出来的图表, 都天生就自带一些功能, 这些功能是每一个图表都具备的, 我们可以通过配置, 对这些功能进行设置

+ 标题: `title `

  ``` js
  var option = { 
      title: { 
          text: "成绩", // 标题文字 
          textStyle: { 
              color: 'red' // 文字颜色 
          },
          borderWidth: 5, // 标题边框 
          borderColor: 'green', // 标题边框颜色 
          borderRadius: 5, // 标题边框圆角 
          left: 20, // 标题的位置 
          top: 20 // 标题的位置 
      } 
  }
  ```

  ![image-20220822092543787](.\assets\image-20220822092543787.png)

+ 提示框: `tooltip `

  `tooltip` 指的是当鼠标移入到图表或者点击图表时, 展示出的提示框

  + 触发类型: trigger		**可选值有item\axis**

  + 触发时机: triggerOn    **可选值有 mouseOver\click**

  + 格式化显示: formatter  

    + 字符串模板

      ``` js
      var option = { 
          tooltip: { trigger: 'item', triggerOn: 'click', formatter: '{b}:{c}' } 
      }
      这个{b} 和 {c} 所代表的含义不需要去记, 在官方文档中有详细的描述
      ```

      ![image-20220822092828517](.\assets\image-20220822092828517.png)

    + 回调函数

      ``` js
      var option = { 
          tooltip: { 
              	trigger: 'item', 
              	triggerOn: 'click', 
                  formatter: function (arg) { return arg.name + ':' + arg.data } 
          } 
      }
      ```

      ![image-20220822092923863](.\assets\image-20220822092923863.png)

+ 工具按钮: toolbox 

  toolbox 是 ECharts 提供的工具栏, 内置有 导出图片，数据视图, 重置, 数据区域缩放, 动态类型切换五个工具

  工具栏的按钮是配置在 feature 的节点之下

  ``` js
  var option = { 
      toolbox: { 
          feature: { 
              saveAsImage: {}, // 将图表保存为图片 
              dataView: {}, // 是否显示出原始数据 
              restore: {}, // 还原图表 
              dataZoom: {}, // 数据缩放 
              magicType: { // 将图表在不同类型之间切换,图表的转换需要数据的支持 
                  type: ['bar', 'line'] 
              } 
          } 
      } 
  }
  ```

  ![image-20220822093105646](.\assets\image-20220822093105646.png)

+ 图例: legend 

  legend 是图例,用于筛选类别,需要和 series 配合使用

  + legend 中的 data 是一个数组
  + legend 中的 data 的值需要和 series 数组中某组数据的 name 值一致

  ``` js
  var option = { 
      legend: { data: ['语文', '数学'] },
      xAxis: { 
          type: 'category', 
          data: ['张三', '李四', '王五', '闰土', '小明', '茅台', '二妞', '大强'] 
      },
      yAxis: { type: 'value' },
      series: [ 
          { name: '语文', type: 'bar', data: [88, 92, 63, 77, 94, 80, 72, 86] }, 
          {name: '数学', type: 'bar', data: [93, 60, 61, 82, 95, 70, 71, 86] }
      ]
  }
  ```

  ![image-20220822093354478](.\assets\image-20220822093354478.png)

### 3.2 **图表2 折线图**

#### 3.2.1 **折线图的实现步骤**

+ 步骤1 ECharts 最基本的代码结构

  ``` html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head>
          <script src="js/echarts.min.js"></script> 
      </head> 
      <body>
          <div style="width: 600px;height:400px"></div> 
          <script> 
              var mCharts = echarts.init(document.querySelector("div"))
              var option = {}
              mCharts.setOption(option) 
          </script> 
      </body> 
  </html>
  ```

  此时 option 是一个空空如也的对象

+ 步骤2 准备 x 轴的数据

  ``` js
  var xDataArr = ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月']
  ```

+ 步骤3 准备 y 轴的数据

  ``` js
  var yDataArr = [3000, 2800, 900, 1000, 800, 700, 1400, 1300, 900, 1000, 800, 600]
  ```

+ 步骤4 准备 option , 将 series 中的 type 的值设置为: line

  ``` js
  var option = { 
      xAxis: { type: 'category', data: xDataArr },
      yAxis: { type: 'value' },
      series: [ { type: 'line', data: yDataArr } ] 
  }
  ```

最终的效果如下:

![image-20220822094000480](.\assets\image-20220822094000480.png)

#### 3.3.2 **折线图的常见效果**

+ 标记

  + 最大值\最小值 `markPoint `

    ``` js
    var option = { 
        series: [ { 
        ...... markPoint: {
    				data: [ { type: 'max', name: '最大值' }, {type: 'min', name: '最小值' } ] 		} } ] 
    }
    ```

    ![image-20220822094158205](.\assets\image-20220822094158205.png)

  + 平均值 `markLine `

    ``` js
    var option = { 
        series: [ 
            { ...... markLine: { 
                data: [ { type: 'average', name: '平均值' } ] 
            } } 
        ] 
    }
    ```

    ![image-20220822094314394](.\assets\image-20220822094314394.png)

  + 标注区间 `markArea `

    ``` js
    var option = { 
        series: [ 
            { ...... markArea: { data: [ 
                	[ { xAxis: '1月' }, {xAxis: '2月' } ],
                    [ { xAxis: '7月' }, {xAxis: '8月' } ] 
            	]} 
            } 
        ] 
    }
    ```

    ![image-20220822094446872](.\assets\image-20220822094446872.png)

+ 线条控制

  + 平滑线条 smooth 

    ``` JS
    var option = { series: [ { ...... smooth: true } ] }
    ```

    ![image-20220822094533897](.\assets\image-20220822094533897.png)

  + 线条样式 lineStyle

    ``` JS
    var option = { series: [ { ...... smooth: true, lineStyle: { color: 'green', type: 'dashed' // 可选值还有 dotted solid } } ] }
    ```

    ![image-20220822094613878](.\assets\image-20220822094613878.png)

+ 填充风格 areaStyle 

    ``` JS
    var option = { series: [ { type: 'line', data: yDataArr, areaStyle: { color: 'pink' } } ] }
    ```

    ![image-20220822094640240](.\assets\image-20220822094640240.png)

+ 紧挨边缘 boundaryGap 

    boundaryGap 是设置给 x 轴的, 让起点从 x 轴的0坐标开始

    ``` JS
    var option = { xAxis: { type: 'category', data: xDataArr, boundaryGap: false } }
    ```

    ![image-20220822094811412](.\assets\image-20220822094811412.png)
    
+ 缩放, 脱离0值比例

    + 如果每一组数据之间相差较少, 且都比0大很多, 那么有可能会出现这种情况

      ``` js
      var yDataArr = [3005, 3003, 3001, 3002, 3009, 3007, 3003, 3001, 3005, 3004, 3001, 3009] // 此时y轴的数据都在3000附近, 每个数之间相差不多 
      var option = { 
          xAxis: {type: 'category', data: xDataArr },
          yAxis: { type: 'value' },
          series: [ { type: 'line', data: yDataArr } ] 
      }
      ```

      ![image-20220822095030779](.\assets\image-20220822095030779.png)

	 这显然不是我们想要的效果, 因此可以配置上 scale , 让其摆脱0值比例
	+ scale 配置
	
	  scale 应该配置给 y 轴 
	
	  ``` js
	  var option = { yAxis: { type: 'value', scale: true } }
	  ```
	
	  ![image-20220822095129862](.\assets\image-20220822095129862.png)
	
+ 堆叠图

    堆叠图指的是, 同个类目轴上系列配置相同的 stack 值后，后一个系列的值会在前一个系列的值上相加

    如果在一个图表中有两个或者多个折线图, 在没有使用堆叠配置的时候, 效果如下: 
    
    ``` js
    <script> 
        var mCharts = echarts.init(document.querySelector("div")) 
        var xDataArr = ['周一', '周二', '周三', '周四', '周五', '周六', '周日'] 
        var yDataArr1 = [120, 132, 101, 134, 90, 230, 210] 
        var yDataArr2 = [20, 82, 191, 94, 290, 330, 310] 
	    var option = { 
            xAxis: { type: 'category', data: xDataArr },
	        yAxis: { type: 'value', scale: true },
	        series: [ { type: 'line', data: yDataArr1 },{ type: 'line', data: yDataArr2 } ] 
	    }
	    mCharts.setOption(option) 
	</script>
	```
	
	![image-20220822095254472](.\assets\image-20220822095254472.png)
	
	使用了堆叠图之后:
	
	```js
	var option = { 
	    series: [ 
	        { 
	            type: 'line', 
	         	data: yDataArr1, 
	         	stack: 'all' // series中的每一个对象配置相同的stack值, 这个all可以任 意写 
	        },
	        { 
	            type: 'line', 
	            data: yDataArr2, 
	            stack: 'all' // series中的每一个对象配置相同的stack值, 这个all可以任意 写 
	        } 
	    ] 
	}
	```
	
	 ![image-20220822095437093](E:\vue3_project\new-bee-admin\doc\assets\image-20220822095437093.png)
	
	蓝色这条线的y轴起点, 不再是y轴, 而是红色这条线对应的点. 所以相当于蓝色是在红色这条线的基础之上进行绘制. 基于前一个图表进行堆叠

#### **3.2.3. 折线图的特点**

折线图更多的使用来呈现数据随时间的『变化趋势』



### 3.3 **图表3 **散点图

一般用于表现多条数据的相关性

#### 3.3.1 **散点图的实现步骤**

+ 步骤1 ECharts 最基本的代码结构

  ``` html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head>
          <script src="js/echarts.min.js"></script> 
      </head> 
      <body>
          <div style="width: 600px;height:400px"></div> 
          <script>
              var mCharts = echarts.init(document.querySelector("div")) 
              var option = {} mCharts.setOption(option)
          </script> 
      </body> 
  </html>
  ```

  此时 option 是一个空空如也的对象

+ 步骤2 准备 x 轴和 y 轴的数据

  假设这个数据是从服务器获取到的, 数组中的每一个元素都包含3个维度的数据: 性别,身高,体重, 而散点图需要的数据是一个二维数组, 所以我们需要将从服务器获取到的这部分数据,通过代码生成散点图需要的数据

  ``` js
  var axisData = [] 
  for (var i = 0; i < data.length; i++) { 
      var height = data[i].height 
      var weight = data[i].weight 
      var itemArr = [height, weight] 
      axisData.push(itemArr) 
  }
  ```

  `axisData` 就是一个二维数组, 数组中的每一个元素还是一个数组, 最内层数组中有两个元素, 一个

  代表身高, 一个代表体重

+ 步骤3 准备配置项

  + `xAxis` 和 `yAxis` 的 type 都要设置为 value 

  + 在 series 下设置 `type:scatter`

  ``` js
  var option = { 
      xAxis: { type: 'value' },
      yAxis: { type: 'value' },
      series: [ { type: 'scatter', data: axisData } ] 
  }
  ```

+ 步骤4 调整配置项, 脱离0值比例

  给 xAxis 和 yAxis 配置 scale 的值为 true 

  `scale: true `



#### 3.3.2 **散点图的常见效果**

+ 气泡图效果

  要能够达到气泡图的效果, 其实就是让每一个散点的大小不同, 让每一个散点的颜色不同

  + symbolSize 控制散点的大小
  + itemStyle.color 控制散点的颜色

  这两个配置项都支持固定值的写法, 也支持回调函数的写法

  固定值的写法如下: 

  ``` js
  var option = { 
      series: [ { 
          type: 'scatter', 
          data: axisData, 
          symbolSize: 25, 
          itemStyle: { color: 'green', } 
      } ] 
  }
  ```

  ![image-20220823084756898](.\assets\image-20220823084756898.png)

  回调函数的写法如下:

  ``` js
  var option = { 
      series: [ { 
          type: 'scatter', 
          data: axisData,
          symbolSize: function (arg) { 
              var weight = arg[1] 
              var height = arg[0] / 100 
              // BMI > 28 则代表肥胖, 肥胖的人用大的散点标识, 正常的人用小散点标识 
              // BMI: 体重/ 身高*身高 kg m 
              var bmi = weight / (height * height) 
              if (bmi > 28) { return 20 }
              return 5 
          },
          itemStyle: {
              color: function (arg) { 
                  var weight = arg.data[1] 
                  var height = arg.data[0] / 100 
                  var bmi = weight / (height * height)
                  if (bmi > 28) { return 'red' }
                  return 'green' } 
          } 
      } ] 
  }
  ```

  ![image-20220823084952643](.\assets\image-20220823084952643.png)

  

+ 涟漪动画效果

  + `type:effectScatter`

    将 type 的值从 scatter 设置为 effectScatter 就能够产生涟漪动画的效果

  + rippleEffect 

    rippleEffect 可以配置涟漪动画的大小

    ``` js
    var option = { series: [ { type: 'effectScatter', rippleEffect:{ scale:3 } } ] }
    ```

    ![image-20220823085046879](.\assets\image-20220823085046879.png)

  + showEffectOn 

    showEffectOn 可以控制涟漪动画在什么时候产生, 它的可选值有两个: render 和 emphasis

    `render` 代表界面渲染完成就开始涟漪动画

    `emphasis` 代表鼠标移过某个散点的时候, 该散点开始涟漪动画

  ``` js
  var option = { 
      series: [ { 
          type: 'effectScatter', 
          showEffectOn: 'emphasis', 
          rippleEffect:{ scale:3 } 
      } ] 
  }
  ```

  ![image-20220823085205673](.\assets\image-20220823085205673.png)

#### 3.3.3 **散点图的特点**

散点图可以帮助我们推断出**不同维度数据之间的相关性**, 比如上述例子中,看得出身高和体重是正相关, 身高越高, 体重越重

散点图也经常用在地图的标注上



#### 3.3.4 **直角坐标系的常见配置**

直角坐标系的图表指的是带有x轴和y轴的图表, 常见的直角坐标系的图表有: 柱状图 折线图 散点图 

针对于直角坐标系的图表, 有一些通用的配置

+ 配置1:  网格 grid

  grid是用来控制直角坐标系的布局和大小, x轴和y轴就是在grid的基础上进行绘制的

  + 显示 grid :   show: true

  + grid 的边框:  borderWidth : 10

  + grid 的位置和大小: left top right bottom     width height

    ``` js
    var option = { 
        grid: { 
            show: true, // 显示grid 
            borderWidth: 10, // grid的边框宽度 
            borderColor: 'red', // grid的边框颜色 
            left: 100, // grid的位置 
            top: 100, 
            width: 300, // grid的大小 
            height: 150 
        } 
    }
    ```

+ 配置2: 坐标轴 axis

  坐标轴分为x轴和y轴, 一个 grid 中最多有两种位置的 x 轴和 y 轴

  + 坐标轴类型 type 

    `value` : 数值轴, 自动会从目标数据中读取数据

    `category` : 类目轴, 该类型必须通过 data 设置类目数据

  + 坐标轴位置

    `xAxis` : 可取值为 top 或者 bottom 

    `yAxis` : 可取值为 left 或者 right 

  ``` js
  var option = { 
      xAxis: { type: 'category', data: xDataArr, position: 'top' },
      yAxis: { type: 'value', position: 'right' } 
  }
  ```

+ 配置3: 区域缩放 dataZoom

  `dataZoom` 用于区域缩放, 对数据范围过滤, x轴和y轴都可以拥有, dataZoom 是一个数组, 意味着可以配置多个区域缩放器

  + 区域缩放类型 type 

    slider : 滑块

    inside : 内置, 依靠鼠标滚轮或者双指缩放

  + 产生作用的轴

    xAxisIndex :设置缩放组件控制的是哪个 x 轴, 一般写0即可

    yAxisIndex :设置缩放组件控制的是哪个 y 轴, 一般写0即可

  + 指明初始状态的缩放情况

    start : 数据窗口范围的起始百分比

    end : 数据窗口范围的结束百分比

  ``` js
  var option = { 
      xAxis: { type: 'category', data: xDataArr },
      yAxis: { type: 'value' },
      dataZoom: [ 
          { type: 'slider', xAxisIndex: 0 },
          { type: 'slider', yAxisIndex: 0, start: 0, end: 80 } 
      ] 
  }
  ```

  ![image-20220827091453188](.\assets\image-20220827091453188.png)

需要注意的是, 针对于非直角坐标系图表, 比如饼图 地图 等, 以上三个配置可能就不会生效了


### 3.4 图表4 饼图

#### 3.4.1 **饼图的实现步骤**

+ 步骤1 ECharts 最基本的代码结构

  ``` html
  <div style="width: 600px;height:400px"></div> 
  <script> 
      var mCharts = echarts.init(document.querySelector("div")) 
      var option = {} 
      mCharts.setOption(option) 
  </script>
  ```

  此时 option 是一个空空如也的对象

+ 步骤2 准备数据

  ``` js
  var pieData = [ 
      { value: 11231, name: "淘宝", },
      { value: 22673, name: "京东" },
      { value: 6123, name: "唯品会" },
      { value: 8989, name: "1号店" },
      { value: 6700, name: "聚美优品" }
  ]
  ```

+ 步骤3 准备配置项 在 series 下设置 type:pie 

  ``` js
  var option = { series: [ { type: 'pie', data: pieData } ] }
  ```

![image-20220827091725628](.\assets\image-20220827091725628.png)

注意:

+ 饼图的数据是由 name 和 value 组成的字典所形成的数组
+ 饼图无须配置 xAxis 和 yAxis

#### 3.4.2 **饼图的常见效果**

+ 显示数值

  + `label.show` : 显示文字
  + `label.formatter` : 格式化文字

  ``` js
  var option = { 
      series: [ { 
          type: 'pie', 
          data: pieData, 
          label: { 
              show: true, 
              formatter: function (arg) { 
                  return arg.data.name + '平台' + arg.data.value + '元\n' + arg.percent + '%' 
              } 
          } 
      } ] 
  }
  ```

+ 南丁格尔图

  南丁格尔图指的是每一个扇形的半径随着数据的大小而不同, 数值占比越大, 扇形的半径也就越大

  + `roseType:'radius' `

  ``` js
  var option = { 
      series: [{ 
          type: 'pie', 
          data: pieData, 
          label: { 
              show: true, 
              formatter: function (arg) { 
                  return arg.data.name + '平台' + arg.data.value + '元\n' + arg.percent + '%' } 			},
          roseType: 'radius' 
      } ] 
  }
  ```

  ![image-20220827092049108](.\assets\image-20220827092049108.png)

+ 选中效果

  + `selectedMode: 'multiple'`

    选中模式，表示是否支持多个选中，默认关闭，支持布尔值和字符串，字符串取值可选 'single' ， 'multiple' ，分别表示单选还是多选

  + `selectedOffset: 30`

    选中扇区的偏移距离

    ``` js
    var option = { 
        series: [ 
            { 
                type: 'pie', 
                data: pieData, 
                selectedMode: 'multiple', // 
                selectedOffset: 30 
            } ] 
    }
    ```

  ![image-20220827092221023](.\assets\image-20220827092221023.png)

+ 圆环

  + `radius`

  饼图的半径。可以为如下类型：

  `number `：直接指定外半径值。 

  `string` ：例如， '20%' ，表示外半径为可视区尺寸（容器高宽中较小一项）的 20% 长度。

  ` Array` ：数组的第一项是内半径，第二项是外半径, 通过 Array , 可以将饼图设置为圆环图

  ``` js
  var option = { series: [ { type: 'pie', data: pieData, radius: ['50%', '70%'] } ] }
  ```

  ![image-20220827092424868](.\assets\image-20220827092424868.png)

#### 3.4.3 **饼图的特点**

饼图可以很好地帮助用户快速了解不同分类的数据的**占比情况**



### 3.5 **图表**5 **地图**

#### 3.5.1 **地图图表的使用方式**

百度地图API : 使用百度地图的 api , 它能够在线联网展示地图, 百度地图需要申请 ak 

矢量地图 : 可以离线展示地图, 需要开发者准备矢量地图数据



#### 3.5.2 **矢量地图的实现步骤**

+ 步骤1 ECharts 最基本的代码结构

  ``` html
  <div style="width: 600px;height:400px"></div>
  <script>
      var mCharts = echarts.init(document.querySelector("div")) 
      var option = {} mCharts.setOption(option) 
  </script>
  ```

  此时 option 是一个空空如也的对象

+ 步骤2 准备中国的矢量 json 文件, 放到 json/map/ 目录之下

+ 步骤3 使用 Ajax 获取 china.json 

  ``` js
  $.get('json/map/china.json', function (chinaJson) { })
  ```

+ 步骤4 在Ajax的回调函数中, 往 echarts 全局对象注册地图的 json 数据

  `echarts.registerMap('chinaMap', chinaJson) `

  ``` js
  $.get('json/map/china.json', function (chinaJson) { 
      echarts.registerMap('chinaMap', chinaJson) 
  })
  ```

+ 步骤5 获取完数据之后, 需要配置 geo 节点, 再次的` setOption `

  `type : 'map' `

  `map : 'chinaMap' `

  ``` js
  var mCharts = echarts.init(document.querySelector("div")) 
  $.get('json/map/china.json', function (chinaJson) { 
      echarts.registerMap('chinaMap', chinaJson) 
      var option = { 
          geo: {
              type: 'map',// map是一个固定的值 
              map: 'chinaMap',//chinaMap需要和registerMap中的第一个参数保持一致 
          } 
      };
      mCharts.setOption(option) 
  })
  ```

  ![image-20220827092911723](.\assets\image-20220827092911723.png)

注意: 需要注意的是, 由于在代码中使用了 Ajax , 所以, 关于此文件的打开, 不能以 file 的协议打开, 应该将其置于 HTTP 的服务之下方可正常展示地图

#### 3.5.3 **地图的常见配置**

+ 缩放拖动: `roam`

  ``` js
  var option = { 
      geo: {
          type: 'map',// map是一个固定的值 
          map: 'chinaMap',//chinaMap需要和registerMap中的第一个参数保持一致, 
          roam: true, // 运行使用鼠标进行拖动和缩放 
      } 
  }
  ```

+ 名称显示: `label`

  ``` js
  var option = {
      geo: {
          type: 'map',// map是一个固定的值 
          map: 'chinaMap',//chinaMap需要和registerMap中的第一个参数保持一致, 
          roam: true, 
          label: { show: true } 
      } 
  }
  ```

  ![image-20220827093117689](.\assets\image-20220827093117689.png)

+ 初始缩放比例:` zoom`    

  ``` js
  zoom: 0.8, // 地图的缩放比例, 大于1代表放大, 小于1代表缩小
  ```

+ 地图中心点: `center`

  ``` js
  center: [87.617733, 43.792818] // 当前视角的中心点，用经纬度表示
  ```



#### 3.4.4 **地图的常见效果**

##### 显示某个区域

1. 准备安徽省的矢量地图数据

2. 加载安徽省地图的矢量数据

   ``` js
   $.get('json/map/anhui.json', function (anhuiJson) { })
   ```

3. 在Ajax的回调函数中注册地图矢量数据

   ``` js
   echarts.registerMap('anhui', anhuiJson)
   ```

4. 配置 geo 的 type:'map' , map:'anhui

5. 通过 zoom 调整缩放比例

6. 通过 center 调整中心点

``` js
var mCharts = echarts.init(document.querySelector("div")) 
$.get('json/map/anhui.json', function (anhuiJson) { 
    console.log(anhuiJson) 
    echarts.registerMap('anhui', anhuiJson) 
    var option = { 
        geo: {
			type: 'map', 
        	map: 'anhui', 
        	label: { show: true },
        	zoom: 1.2, 
        	center: [116.507676, 31.752889] 
    	}
    };
    mCharts.setOption(option) 
})
```



##### 不同城市颜色不同

1. 显示基本的中国地图

2. 准备好城市空气质量的数据, 并且将数据设置给 series 
   ``` js
   var airData = [{ name: '北京', value: 39.92 }] ...... 
   var option = { ...... series: [ { data: airData } ] }
   ```

3. 将 series 下的数据和 geo 关联起来

   ``` js
   var option = { series: [ { data: airData, geoIndex: 0, type: 'map' } ] }
   ```

4. 结合 `visualMap` 配合使用

   visualMap 是视觉映射组件, 和之前区域缩放 dataZoom 很类似, 可以做数据的过滤. 只不过dataZoom 主要使用在直角坐标系的图表, 而 visualMap 主要使用在地图或者饼图中

   ``` js
   var option = {
       visualMap: { 
           min: 0, // 最小值 
           max: 300, // 最大值 
           inRange: { 
               color: ['white', 'red'] // 颜色的范围 
           },
           calculable: true // 是否显示拖拽用的手柄（手柄能拖拽调整选中范围） 
       }
   }
   ```

   ![image-20220827093720394](.\assets\image-20220827093720394.png)

##### 地图和散点图结合

1. 给 series 这个数组下增加新的对象

2. 准备好散点数据,设置给新对象的 data

   ``` js
   var scatterData = [ { value: [117.283042, 31.86119] // 散点的坐标, 使用的是经纬度 } ]
   ```

3. 配置新对象的 type

   type:effectScatter

4. 让散点图使用地图坐标系统

   coordinateSystem: 'geo'

5. 让涟漪的效果更加明显

   rippleEffect: { scale: 10 }

``` js
var option = { 
    series: [ 
        { data: airData, geoIndex: 0, type: 'map' }, 
        { 
            data: scatterData, 
            type: 'effectScatter', 
            coordinateSystem: 'geo', 
            rippleEffect: { scale: 10 } 
        } 
    ] 
}
```

![image-20220827093918640](.\assets\image-20220827093918640.png)



#### 3.4.5 **地图的特点**

地图主要可以帮助我们从宏观的角度快速看出不同**地理位置**上数据的差异



### 3.6 图表6 **雷达图**

#### 3.6.1 **雷达图的实现步骤**

+ 步骤1 ECharts 最基本的代码结构

+ 步骤2 定义各个维度的最大值

  ``` js
  var dataMax = [
      { name: '易用性', max: 100 },
      { name: '功能', max: 100 },
      { name: '拍照', max: 100 },
      { name: '跑分', max: 100 },
      { name: '续航', max: 100 } 
  ]
  ```

+ 步骤3 准备具体产品的数据

  ``` js
  var hwScore = [80, 90, 80, 82, 90] 
  var zxScore = [70, 82, 75, 70, 78]
  ```

+ 步骤4 在 series 下设置 type:radar 

  ``` js
  var option = { 
      radar: { indicator: dataMax },
      series: [ 
          { 
              type: 'radar', 
              data: [ 
                  { name: '华为手机1', value: hwScore },
                  { name: '中兴手机1', value: zxScore } 
              ] 
          } 
      ]
  }
  ```

  ![image-20220827094153332](.\assets\image-20220827094153332.png)

#### 3.6.2 **雷达图的常见效果**

+ 显示数值 label 

  ``` js
  var option = { 
      series: [ 
          { type: 'radar', label: { show: true } ... } 
      ] 
  }
  ```

+ 区域面积 areaStyle 

  ![image-20220827094319217](.\assets\image-20220827094319217.png)

+ 绘制类型 shape

  雷达图绘制类型，支持 'polygon' 和 'circle' 

  `polygon`: 多边形    `circle `圆形

#### 3.6.3 **雷达图的特点**

雷达图可以用来分析多个维度的数据与标准数据的对比情况



### 3.7 图表7 **仪表盘图**

#### 3.7.1 **仪表盘的实现步骤**

+ 步骤1 ECharts 最基本的代码结构
+ 步骤2: 准备数据, 设置给 series 下的 data     `data:[97]`
+ 步骤3: 在 series 下设置 `type:gauge `

``` js
var option = { series: [ { type: 'gauge', data: [{ value: 97, }] } ] }
```

![image-20220827094527258](.\assets\image-20220827094527258.png)



#### 3.7.2 **仪表盘的常见效果**

+ 数值范围: max min
+ 多个指针: 增加data中数组的元素
+ 多个指针颜色的差异: itemStyle

``` js
var option = { 
	series: [ 
        { 
            type: 'gauge', 
            data: [
                { value: 97, itemStyle: { color: 'pink' } }, 
                { value: 85, itemStyle: { color: 'green' } }
            ], 
            min: 50 
        } 
    ] 
}
```

![image-20220827094637493](.\assets\image-20220827094637493.png)

#### 3.7.3 **仪表盘的特点**

仪表盘可以更直观的表现出某个指标的进度或实际情况



### 4. **配置项小结**

#### 4.1 **柱状图** **bar**

| **series[].type** | **xAxis** | **yAxis** | **markPoint** | **markLine** | **label** | **barWidth** |
| ----------------- | --------- | --------- | ------------- | ------------ | --------- | ------------ |
| 图表类型          | x轴       | y轴       | 最大值/最小值 | 平均值       | 显示文本  | 柱宽度       |

#### 4.2 **折线图** **line**

| **series[].type** | **xAxis** | **yAxis** | **markPoint** | **markLine** | **label** | **smooth** |
| ----------------- | --------- | --------- | ------------- | ------------ | --------- | ---------- |
| 图表类型          | x轴       | y轴       | 最大值/最小值 | 平均值       | 显示文本  | 平滑线     |

| areaStyle | **lineStyle** | **boundaryGap** | **scale**   |
| --------- | ------------- | --------------- | ----------- |
| 风格x轴   | 线条风格      | 紧挨边缘        | 脱离0值比例 |

#### 4.3 **散点图** **scatter**

| **series[].type** | **xAxis** | yAxis | **symbolSize** |
| ----------------- | --------- | ----- | -------------- |
| 图表类型          | x轴       | y轴   | 散点大小       |

| itemStyle | showEffectOn | rippleEffect | **scale**   |
| --------- | ------------ | ------------ | ----------- |
| 散点样式  | 显示时机     | 涟漪效果     | 脱离0值比例 |

#### 4.4 **饼图** **pie**

| **series[].type** | label    | radius | roseType | selectMode | selectOffset   |
| ----------------- | -------- | ------ | -------- | ---------- | -------------- |
| 图表类型          | 显示文本 | 半径   | 饼图类型 | 是否多选   | 选中扇区偏移量 |

#### 4.5 **地图** **map**

![image-20220827095753210](.\assets\image-20220827095753210.png)

#### 4.6 **雷达图** **radar**

![image-20220827095807238](.\assets\image-20220827095807238.png)

#### 4.7 **仪表盘** **gauge**

![image-20220827095820758](.\assets\image-20220827095820758.png)

#### 4.8 **直角坐标系配置**

+ grid

  ![image-20220827095857555](.\assets\image-20220827095857555.png)

+ axis

  ![image-20220827095913583](.\assets\image-20220827095913583.png)

+ dataZoom

  ![image-20220827095926668](.\assets\image-20220827095926668.png)

#### 4.9 **通用配置**

+ title

  ![image-20220827100036629](.\assets\image-20220827100036629.png)

+ tooltip

  ![image-20220827100050230](.\assets\image-20220827100050230.png)

+ toolbox.feature

  ![image-20220827100103916](.\assets\image-20220827100103916.png)

+ legend

  ![image-20220827100121828](.\assets\image-20220827100121828.png)

## 二、高级篇

### 1. 主题

#### 1.1 默认主题

ECharts 中默认内置了两套主题: `light` `dark`

在初始化对象方法 init 中可以指明

``` js
var chart = echarts.init(dom, 'light') 
var chart = echarts.init(dom, 'dark')
```



#### 1.2 自定义主题

1. 在主题编辑器中编辑主题

   主题编辑器的地址为: `https://www.echartsjs.com/theme-builder/`

2. 下载主题, 是一个 js 文件

   在线编辑完主题之后, 可以点击下载主题按钮, 下载主题的js文件

3. 引入主题 js 文件

   ``` html
   <script src="js/echarts.min.js"></script> 
   <script src="js/theme.js"></script>
   ```

4. 在 init 方法中使用主题

   ``` js
   var mCharts = echarts.init(document.querySelector("div"), 'theme')
   ```

### 2. 调色盘

它是一组颜色，图形、系列会自动从其中选择颜色, 不断的循环从头取到尾, 再从头取到尾, 如此往复

#### 2.1 主题调色盘

``` js
echarts.registerTheme('theme', { 
    "color": [ 
        "#893448", 
        "#d95850", 
        "#eb8146", 
        "#ffb248", 
        "#f2d643", 
        "#ebdba4" 
    ],
    "backgroundColor": "rgba(242,234,191,0.15)", 
    ......
})
```

#### 2.2  全局调色盘

全局调色盘是在 option 下增加一个 color 的数组

``` js
var option = { 
    // 全局调色盘 
    color: ['red', 'green', 'blue'], 
    ...... 
}
mCharts.setOption(option)
```

#### 2.3 局部调色盘

局部调色盘就是在 `series` 下增加一个` color `的数组

``` js
var option = { 
    // 全局调色盘 
    color: ['red', 'green', 'blue'], 
    series: [ 
        { 
            type: 'pie', 
            data: pieData, // 局部调色盘 
            color: ['pink', 'yellow', 'black'] 
        } 
    ] 
}
mCharts.setOption(option)
```

需要注意一点的是, 如果全局的调色盘和局部的调色盘都设置了, 局部调色盘会产生效果, 这里面遵循的是就近原则

#### 2.4 渐变颜色的实现

在` ECharts `中, 支持线性渐变和径向渐变两种颜色渐变的方式

+ 线性渐变

  线性渐变的类型为 linear , 他需要配置线性的方向, 通过 x, y, x2, y2 

  即可进行配置x , y , x2 , y2 , 范围从 0 - 1

  相当于在图形包围盒中的百分比，如果 global 为 true ，则该四个值是绝对的像素位置

  ``` js
  series: [ 
      { 
          type: 'bar', 
          data: yDataArr,
          itemStyle: { 
              color: { 
                  type: 'linear', 
                  x: 0, 
                  y: 0, 
                  x2: 0,
                  y2: 1,
                  colorStops: [
                      // 0% 处的颜色
                      { offset: 0, color: 'red'  }, 
                      // 100% 处的颜色 
                      {offset: 1, color: 'blue' }
                  ], 
                  globalCoord: false // 缺省为 false 
              } } } ]
  ```

  ![image-20220831104331611](.\assets\image-20220831104331611.png)
  
+ 径向渐变

  线性渐变的类型为 radial , 他需要配置径向的方向, 通过 x , y , r 即可进行配置

  前三个参数分别是圆心 x , y 和半径，取值同线性渐变

  在下述代码中的 0.5 0.5 0.5 意味着从柱的重点点, 向外径向扩散半径为宽度一半的圆

  ``` js
  series: [ 
      { 
          itemStyle: { 
              color: { 
                  type: 'radial', 
                  x: 0.5, 
                  y: 0.5, 
                  r: 0.5, 
                  colorStops: [
                      // 0% 处的颜色
                      { offset: 0, color: 'red'  }, 
                      // 100% 处的颜色
                      {offset: 1, color: 'blue'  }
                  ], 
                  global: false // 缺省为 false 
              } 
          } 
      } 
  ]
  ```

  ![image-20220831104526722](.\assets\image-20220831104526722.png)

### 3. 样式

#### 3.1 直接样式

+ `itemStyle`    数据样式
+ `textStyle`    标题样式
+ `lineStyle`    线条样式
+ `areaStyle   `    填充样式
+ `label`             文字样式

``` js
data: [
    { 
        value: 11231, 
        name: "淘宝", 
        itemStyle: { color: 'black' } 
    } 
]

title: { 
    text: '我是标题', 
    textStyle: { color: 'red' } 
}

label: { color: 'green' }
```

这些样式一般都可以设置颜色或者背景或者字体等样式, 他们会覆盖主题中的样式

#### 3.2 高亮样式

图表中, 其实有很多元素都是有两种状态的, 一种是**默认状态**, 另外一种就是鼠标滑过或者点击形成的高亮状态. 而**高亮样式**是针对于元素的高亮状态设定的样式

那它的使用也非常简单,在 emphasis 中包裹原先的 itemStyle 等等, 我们来试一下

``` js
series: [
    { 
        type: 'pie', 
        label: { color: 'green' },
        emphasis: { label: { color: 'red' }, }, 
        data: [
            { 
                value: 11231, 
                name: "淘宝", 
                itemStyle: { color: 'black' },
                emphasis: { itemStyle: { color: 'blue' }, } 
            }
        ]
    }
]
```

### 4. 自适应

1. 步骤1: 监听窗口大小变化事件
2. 步骤2: 在事件处理函数中调用 ECharts 实例对象的 resize 即可

``` html
<!DOCTYPE html> 
<html lang="en"> 
    <head>
        <script src="js/echarts.min.js"></script> 
    </head> 
    <body>
        <div style=" height:400px;border:1px solid red"></div> 
        <script> 
            var mCharts = echarts.init(document.querySelector("div")) 
            var xDataArr = ['张三', '李四', '王五', '闰土', '小明', '茅台', '二妞', '大 强']
            var yDataArr = [88, 92, 63, 77, 94, 80, 72, 86]
            var option = { 
                xAxis: { type: 'category', data: xDataArr },
                yAxis: { type: 'value' },
                series: [ { type: 'bar', data: yDataArr } ] 
            };

			mCharts.setOption(option) // 监听window大小变化的事件
            window.onresize = function () { 
                // 调用echarts示例对象的resize方法 
                mCharts.resize() 
            }
            // window.onresize = mCharts.resize 
        </script> 
    </body> 
</html>
```



### 5. 动画

#### 5.1 加载动画

`ECharts` 已经内置好了加载数据的动画, 我们只需要在合适的时机显示或者隐藏即可

+ 显示加载动画

  ``` js
  mCharts.showLoading() 
  //一般, 我们会在获取图表数据之前 显示加载动画
  ```

  ![image-20220831105421570](.\assets\image-20220831105421570.png)

+ 隐藏加载动画

  ``` js
  mCharts.hideLoading() 
  // 一般, 我们会在获取图表数据之后 隐藏加载动画, 显示图表
  ```

#### 5.2 增量动画

所有数据的更新都通过 setOption 实现, 我们不用考虑数据到底产生了那些变化, ECharts 会找到两组数据之间的差异然后通过合适的动画去表现数据的变化





**数据改变时  自动执行动画**



#### 5.3 动画的配置

+ 开启动画   `animation: true`

+ 动画时长  `animationDuration: 5000`

+ 缓动动画  `animationEasing : 'bounceOut'`

  `linear` ,线性变化, 这样动画效果会很均匀

  `bounceOut` ,这样动画效果会有一个回弹效果

  <img src=".\assets\image-20220831105714881.png" alt="image-20220831105714881" style="zoom:50%;" />

+ 动画阈值 `animationThreshold: 8`

  单种形式的元素数量大于这个阈值时会关闭动画

  

### 6. 交互API

#### 6.1 **全局**echarts 对象

全局 echarts 对象是引入 echarts.js 文件之后就可以直接使用的

+ `echarts.init`    **初始化ECharts实例对象**   **使用主题**

+ `echarts.registerTheme `   **注册主题 **   !!只有注册过的主题,才能在init方法中使用该主题 !!

+ `echarts.registerMap`    **注册地图数据 **  

  ``` js
  $.get('json/map/china.json', function (chinaJson) { 
      echarts.registerMap('china', chinaJson); 
  });
  
  // geo组件使用地图数据 
  var option = { geo: {type: 'map', map: 'china', }, })
  ```
+ `echarts.connect` 

  + 一个页面中可以有多个独立的图表
  + 每一个图表对应一个 ECharts 实例对象
  + connect 可以实现多图关联，传入联动目标为 EChart 实例，支持数组

  **待补充**



#### 6.2 echartsInstance 对象  (实例)

`eChartsInstance` 对象是通过 `echarts.init `方法调用之后得到的

+ `echartsInstance.setOption`

  设置或修改图表实例的配置项以及数据 

  多次调用setOption方法 合并新的配置和旧的配置  会触发增量动画

+ `echartsInstance.resize`

  重新计算和绘制图表 

  一般和window对象的resize事件结合使用 

  ``` js
  window.onresize = function(){ myChart.resize(); }
  ```

+ `echartsInstance.on`     `echartsInstance.off`

  绑定或者解绑事件处理函数

  + 鼠标事件

    常见事件: 'click'、'dblclick'、'mousedown'、'mousemove'、'mouseup' 等 

    ``` js
    // 绑定事件
    mCharts.on('click', function (arg) { // console.log(arg) console.log('饼图被点击了') })
        
        
    // 解绑事件
    mCharts.off('click')
    ```

  + ECharts 事件

    常见事件:  `legendselectchanged`、`datazoom`、`pieselectchanged`、`mapselectchanged` 等

    ``` js
    mCharts.on('legendselectchanged', function (arg) { 
        console.log(arg)
        console.log('图例选择发生了改变...') 
    })
    ```

+ `echartsInstance.dispatchAction` 

  主动触发某些行为, 使用代码模拟用户的行为

  ``` js
  // 触发高亮的行为
  mCharts.dispatchAction({ type: "highlight", seriesIndex: 0, dataIndex: 1 })
  
  // 触发显示提示框的行为 
  mCharts.dispatchAction({ type: "showTip", seriesIndex: 0, dataIndex: 3 })
  ```

+ `echartsInstance.clear`

  清空当前实例，会移除实例中所有的组件和图表

  清空之后可以再次 setOption

+ `echartsInstance.dispose`

  销毁实例

  销毁后实例无法再被使用
