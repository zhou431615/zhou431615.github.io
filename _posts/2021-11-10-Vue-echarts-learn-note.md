---
layout:     post
title:      "Vue-echarts使用教程"
subtitle:   "Vue-echarts学习笔记"
date:       2021-11-10 23:00:00
author:     "QianYe"

tags:
- Vue
---


## Vue-echarts学习笔记

### 一、什么是Echarts？什么是Vue-echarts?

在学习Vue-echarts之前，您需先了解Echarts。Echarts是一个基于 JavaScript [的开源可视化图表库](https://echarts.apache.org/zh/index.html)，其丰富的图表，多种的样式的特点，让其使用广泛。简单来说，Echarts可以将数据以可视化形式（图表）展示出来，让数据更加生动形象，全面直观。其拥有的图表包括常见的折线图、柱状图、饼图、散点图，还有专业的K线图、热力图、树图、雷达图、路径图等。

先了解一下，Echarts有哪些例子吧。 [官网例子](https://echarts.apache.org/examples/zh/index.html#chart-type-line)

![image-20211128140525455](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281405681.png)

您还需阅读Echarts的文档资料，里面介绍了获取Echarts的方式和在项目(开发环境使用npm包管理方式)中引入Echarts的操作流程。由于本项目是Vue-cli开发(version 2.9.6),就不再采用普通的Echart引入方式，选用Vue-echart，开发更方便。

#### 那为什么要使用vue-echarts呢?直接用echarts不好吗？

根据echarts的官方文档，绘画图表的流程是：画一个图表要先新建一个容器，然后在JS中通过getElementById获取这个容器。这是非常原始的JS和html交互，在开发Vue项目时，比较麻烦，不太方便，不符合经常使用vue开发的同学的使用习惯。而vue-echarts则将echarts获取元素的代码进行封装，变成一个组件，减少开发的冗余。使用Vue-echarts，平均每个图可以让我们少写十行左右代码。vue-echarts最主要的就是完成这个使命，剩下的图表配置项我们要自行看echarts的文档。

**Vue-echarts是Apache ECharts 的 Vue.js 组件。**

这里是Vue-echarts的[中文文档](https://github.com/ecomfe/vue-echarts/blob/main/README.zh-Hans.md)。https://github.com/ecomfe/vue-echarts/blob/main/README.zh-Hans.md

### 二、配置Vue-echarts

> 由于我开发项目使用Vue-cli(2.9.6)，后面的开发的配置，都是在此开发环境基础之上，假定您的Vue配置一切正常。

在阅读Apache ECharts和Vue-echarts的文档之后，让我们开始无脑上手操作吧！！！

在安装Vue-echarts之前，请确保您已经安装`@vue/composition-ap`

```
npm i -D @vue/composition-api
```

Step1 安装

```
npm install echarts vue-echarts
```

Step2 进行注册

可以使用全局注册，也可以使用局部注册。为了更小的打包体积，建议使用局部注册从Echarts单个引入图表或组件。若您使用全局注册，您可在任意组件使用

；如若使用局部注册，您只可在当前组件使用。在这里只介绍局部注册的方式。

```js
import Vue from 'vue'
import ECharts from 'vue-echarts'
import { use } from 'echarts/core'
// 手动引入 ECharts 各模块来减小打包体积

import {
  CanvasRenderer
} from 'echarts/renderers'
import {
  BarChart
} from 'echarts/charts'
import {
  GridComponent,
  TooltipComponent
} from 'echarts/components'

use([
  CanvasRenderer,
  BarChart,
  GridComponent,
  TooltipComponent
]);
```

在了解局部注册之后，那就开始操作吧！只有简单一行代码！！

```vue
<v-chart class="chart" :option="option" />
```

再进行一些简单的配置即可

设置一下CSS样式

```
.chart {
  height: 500px;
  } 
```

在设置一下option参数(以简单的折线图为例)

```js
option:{
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      data: [150, 230, 224, 218, 135, 147, 260],
      type: 'line'
    }
  ]
 }
```

到这里，就在页面绘画出一个简单的折线图，看看效果。

![image-20211128140623402](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281406806.png)

### 三、在项目中使用Vue-Echarts

在项目往往需要效果丰富的图表，会设值一系列包括但不限于标题、工具盒、提示框、主题、图例组件、X和Y轴、坐标轴指示器、区域缩放、视觉映射......。

从头到尾，有这么多配置项。

![image-20211128140801115](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281408980.png)

例如，如下例子echart.vue组件，使用了一些基本的配置，并且自定义了主题。（主题文件，可到Echarts官网进行配置，在下载到本项目）

```vue
<template>
  <div>
    <v-chart class="chart" theme="ovilia-green" :option="option1"/>
  </div>
</template>

<script>
import {use} from "echarts/core";
import {CanvasRenderer} from "echarts/renderers";
import {PieChart, BarChart} from "echarts/charts";
import {
  TitleComponent,
  TooltipComponent,
  LegendComponent
} from "echarts/components";
import VChart from "vue-echarts";
// 导入自定义配置的主题
import theme from "../../theme.json"

const {registerTheme} = require("echarts");
 /*设置绘画图表的各种图表、提示工具组件*/
use([
  CanvasRenderer,
  PieChart,
  BarChart,
  TitleComponent,
  TooltipComponent,
  LegendComponent
]);

//注册自定义主题
registerTheme("ovilia-green", theme);
    
  export default {
  name: "echart",
  components: {
    VChart
  }, data() {
    return {
       option1: {
           //设置标题
        title: {
          text: "2021年计算机系专业招生情况",
          left: "center"
        },
        // 设置提示框
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c}"
        },
           // 设置X轴
        xAxis: {
          type: 'category',
          data: ['计算机科学与技术', '软件工程', '物联网工程', '网络工程', '信息安全',],
          axisPointer:
            {
              show: true,
              type: 'line',
            }

        },
           // 设置Y轴
        yAxis: {
          type: 'value',
          axisPointer: {
            show: true,
            type: 'line',
            snap: true,
          }
        },
        // 添加图表的文字说明(图例组件)
        legend: {
          orient: "vertical",
          left: "left",
          data: [
            "计算机科学与技术",
            "软件工程",
            "物联网工程",
            "网络工程",
            "信息安全"
          ]
        },
        series: [
          {
            name: "计算机系",
            type: "bar",
            radius: "40%",
            center: ["50%", "50%"],
            data: [
              {value: 135, name: "计算机科学与技术"},
              {value: 110, name: "软件工程"},
              {value: 134, name: "物联网工程"},
              {value: 135, name: "网络工程"},
              {value: 148, name: "信息安全"}
            ],
            // 强调某一数据的样式
            emphasis: {
              itemStyle: {
                // color: "rgba(161,8,8,0.5)" ,
                shadowBlur: 8,
                shadowOffsetX: 0,
                shadowColor: "rgba(112,112,112,0.5)"
              }
            }
          }
        ]
      },
    }
  }

}
</script>
<style scoped>
.chart {
  height: 500px;
  background-color: #fffdfb;
  width: 800px;
}
</style>
```

来一起，看看效果吧。

![image-20211128141250804](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281412194.png)

最后，来看看一个完整的案例,几乎使用到所有配置项(以折线图为例)

![image-20211128140925649](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281409353.png)

思考一下，这张图使用那些配置？？

[可以去到配置项找一找答案](https://echarts.apache.org/zh/option.html#title)  

最后，还可以去[下载官方主题或者自定义主题→](https://echarts.apache.org/zh/download-theme.html)

### 四、更加灵活的使用Vue-Echarts

参考github上的代码，总结归纳一下[github地址→](https://github.com/ecomfe/vue-echarts/tree/main/src/demo)

```vue
 <template>
  <main>
 <!-- 条形图 -->
    <h2 id="bar">
      <a href="#bar">Bar chart <small>(with async data &amp; custom theme)</small></a>
      <button
        :class="{
          round: true,
          expand: expand.bar
        }"
        @click="expand.bar = !expand.bar"
        aria-label="toggle"
      ></button>
    </h2>
    <section v-if="expand.bar">
      <figure>
        <v-chart
          :option="bar"
          :init-options="initOptions"
          ref="bar"
          theme="ovilia-green"
          autoresize
          :loading="barLoading"
          :loadingOptions="barLoadingOptions"
          @zr:click="handleZrClick"
          @click="handleClick"
        />
      </figure>
      <p v-if="seconds <= 0"><small>Loaded.</small></p>
      <p v-else>
        <small
        >Data coming in <b>{{ seconds }}</b> second{{
            seconds > 1 ? "s" : ""
          }}...</small
        >
      </p>
      <p>
        <button @click="refresh" :disabled="seconds > 0">Refresh</button>
      </p>
    </section>
  </main>
</template>
```

导入部分(关键部分)

```
// 引入getbar.js
import getBar from "./data/bar";
// registering custom theme
registerTheme("ovilia-green", theme);
```

配置项

```js
export default {
  components: {
    VChart
  },
  data() {
    const options = qs.parse(location.search, { ignoreQueryPrefix: true });
    return {
      options,
      bar: getBar(),
      // 其他配置
      ........
      }
    }
  }
```

最后，关于加载:option="bar"，使用getBar.js进行封装一下，在data() { return {}}  中引用，避免过度冗余。这是getBar.js

```
function random() {
  return Math.round(300 + Math.random() * 700) / 10;
}

export default function getData() {
  return {
    textStyle: {
      fontFamily: 'Inter, "Helvetica Neue", Arial, sans-serif'
    },
    dataset: {
      dimensions: ["Product", "2015", "2016", "2017"],
      source: [
        {
          Product: "Matcha Latte",
          2015: random(),
          2016: random(),
          2017: random()
        },
        {
          Product: "Milk Tea",
          2015: random(),
          2016: random(),
          2017: random()
        },
        {
          Product: "Cheese Cocoa",
          2015: random(),
          2016: random(),
          2017: random()
        },
        {
          Product: "Walnut Brownie",
          2015: random(),
          2016: random(),
          2017: random()
        }
      ]
    },
    xAxis: { type: "category" },
    yAxis: {},
    // Declare several bar series, each will be mapped
    // to a column of dataset.source by default.
    series: [{ type: "bar" }, { type: "bar" }, { type: "bar" }]
  };
}

```

### 五、其他

之后，还有一些应用型的内容，或更加复杂的配置，如

- [ ] 数据集与数据转换的问题

- [ ] 视觉映射的问题

- [ ] 时间与行为(鼠标点击或代码触发)

- [ ] 处理动态的异步数据

- [ ] 一些跨平台的方案(微信小程序)

  如果想更进一步掌握Echarts，您还需要掌握以上内容。

  
