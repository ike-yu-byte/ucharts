![logo](https://img-blog.csdnimg.cn/4a276226973841468c1be356f8d9438b.png)

<!-- [![star](https://gitee.com/uCharts/uCharts/badge/star.svg?theme=gvp)](https://gitee.com/uCharts/uCharts/stargazers)
[![fork](https://gitee.com/uCharts/uCharts/badge/fork.svg?theme=gvp)](https://gitee.com/uCharts/uCharts/members)
[![License](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![npm package](https://img.shields.io/npm/v/@qiun/ucharts.svg?style=flat-square)](https://www.npmjs.com/~qiun) -->

## ike-ucharts 简介

`uCharts`是一款基于`canvas API`开发的适用于所有前端应用的图表库，开发者编写一套代码，可运行到 Web、iOS、Android（基于 uni-app
/
taro ）、以及各种小程序（微信/支付宝/百度/头条/飞书/QQ/快手/钉钉/淘宝）、快应用等更多支持 canvas
API 的平台。ike-ucharts 是 ucharts 的非 uni_modules 版本，支持 npm 方式安装，兼容 vue2 和 vue3 版本的 uniapp 开发。

## ucharts 官方网站

## [https://www.ucharts.cn](https://www.ucharts.cn)

## 快速体验

一套代码编到多个平台，依次扫描二维码，亲自体验 uCharts 图表跨平台效果！其他平台请自行编译。

![](https://www.ucharts.cn/images/web/guide/qrcode20220224.png)

![](https://img-blog.csdnimg.cn/7d0115593ff24ac39a224fb7c6ed72a4.png)

## 快速开始

安装

```
npm install ike-ucharts
```

js 部分

```
import { ref, watch } from 'vue';
import { onShow } from '@dcloudio/uni-app';
import ucharts from 'ike-ucharts';
const props = defineProps({
  data: {
    type: Object,
    default: () => ({
      categories: [
        '2000',
        '2001',
        '2002',
        '2003',
        '2004',
        '2005',
        '2006',
        '2007',
        '2008',
        '2009',
        '2010',
        '2011',
        '2012',
        '2013',
        '2014',
        '2015',
        '2016',
        '2017',
        '2018',
        '2019',
        '2020',
      ],
      series: [
        {
          name: '',
          data: [
            35, 8, 25, 37, 4, 20, 35, 8, 25, 37, 4, 20, 35, 8, 25, 37, 4, 20,
            11, 20, 15,
          ],
        },
      ],
    }),
  },
  showLegend: {
    type: Boolean,
    default: false,
  },
})

const chartData = ref(JSON.parse(JSON.stringify(props.data)))

// 监听数据变化从而更新图形
watch(
  () => props.data,
  (val) => {
    chartData.value = JSON.parse(JSON.stringify(val))
  },
  {
    immediate: true,
    deep: true,
  },
)

onShow(() => {
  // 屏幕尺寸变化时更新数据重绘图形
  const windowResizeCallback = () => {
    chartData.value = JSON.parse(JSON.stringify(props.data))
  };
  uni.onWindowResize(windowResizeCallback);
})

const opts = {
  // width: '100%',
  // height: '100%',
  color: [
    // '#1890FF',
    '#F7941A', // 黄色
    '#91CB74',
    '#FAC858',
    '#EE6666',
    '#73C0DE',
    '#3CA272',
    '#FC8452',
    '#9A60B4',
    '#ea7ccc',
  ],
  dataLabel: false, // 隐藏线上面数据文字显示
  dataPointShape: false, // 隐藏数据节点
  padding: [0, 0, 0, 0],
  enableScroll: false,
  legend: {
    show: false,
  },
  xAxis: {
    disableGrid: true,
    disabled: true,
    axisLine: false, // 坐标轴线
    fontColor: 'transparent',
  },
  yAxis: {
    gridType: 'dash',
    dashLength: 2,
    disabled: true,
    gridColor: 'transparent',
    data: {
      0: {
        fontColor: 'transparent',
      },
    },
  },
  extra: {
    area: {
      type: 'curve', // straight: 直线，curve：曲线
      opacity: 0.2,
      addLine: true,
      width: 2,
      gradient: false,
      activeType: 'hollow',
    },
    tooltip: {
      showBox: false
    }
  },
}
```

html 部分

```
<div class="chart-box">
    <ucharts type="area" :chartData="chartData" :opts="opts" />
</div>
```

css 部分

```
.chart-box {
  width: 100%;
  height: 100%;
}
```

## easycom 导入组件
为了兼容H5以外的平台，必须采用easycom的方式导入vue组件
```
"easycom": {
  // 自动导入组件
  "autoscan": true,
  "custom": {
    // uni-ui 规则如下配置
    "^uni-(.*)": "@dcloudio/uni-ui/lib/uni-$1/uni-$1.vue",
    // uview-plus规则如下配置
    "^u--(.*)": "uview-plus/components/u-$1/u-$1.vue",
    "^up-(.*)": "uview-plus/components/u-$1/u-$1.vue",
    "^u-([^-].*)": "uview-plus/components/u-$1/u-$1.vue",
    // wot-degign-uni配置如下所示
    "^wd-(.*)": "wot-design-uni/components/wd-$1/wd-$1.vue",
    // "^ike-(.*)": "common-components/components/ike-$1/ike-$1.vue",
    // ucharts相关
    "^qiun-(.*)": "ike-ucharts/components/qiun-$1/qiun-$1.vue"
  }
}
```

## 视频教程

## [uCharts 新手入门教程](https://www.bilibili.com/video/BV1qA411Q7se/?share_source=copy_web&vd_source=42a1242f9aaade6427736af69eb2e1d9)

#### 教程链接

[官网组件使用教程](https://www.ucharts.cn/v2/#/tool/index)

## 版权信息

uCharts 始终坚持开源，遵循
[Apache Licence 2.0](https://www.apache.org/licenses/LICENSE-2.0.html)
开源协议，意味着您无需支付任何费用，即可将 uCharts 应用到您的产品中。

注意：这并不意味着您可以将 uCharts 应用到非法的领域，比如涉及赌博，暴力等方面。如因此产生纠纷或法律问题，uCharts 相关方及秋云科技不承担任何责任。

## 合作伙伴

[![DIY官网](https://www.ucharts.cn/images/web/guide/links/diy-gw.png)](https://www.diygw.com/)
[![HasChat](https://www.ucharts.cn/images/web/guide/links/haschat.png)](https://gitee.com/howcode/has-chat)
[![uViewUI](https://www.ucharts.cn/images/web/guide/links/uView.png)](https://www.uviewui.com/)
[![图鸟UI](https://www.ucharts.cn/images/web/guide/links/tuniao.png)](https://ext.dcloud.net.cn/plugin?id=7088)
[![thorui](https://www.ucharts.cn/images/web/guide/links/thorui.png)](https://ext.dcloud.net.cn/publisher?id=202)
[![FirstUI](https://www.ucharts.cn/images/web/guide/links/first.png)](https://www.firstui.cn/)
[![nProUI](https://www.ucharts.cn/images/web/guide/links/nPro.png)](https://ext.dcloud.net.cn/plugin?id=5169)
[![GraceUI](https://www.ucharts.cn/images/web/guide/links/grace.png)](https://www.graceui.com/)

## 相关链接

- [uCharts 官网](https://www.ucharts.cn)
- [DCloud 插件市场地址](https://ext.dcloud.net.cn/plugin?id=271)
- [uCharts 码云开源托管地址](https://gitee.com/uCharts/uCharts)
  [![star](https://gitee.com/uCharts/uCharts/badge/star.svg?theme=gvp)](https://gitee.com/uCharts/uCharts/stargazers)
- [uCharts npm 开源地址](https://www.ucharts.cn)
- [ECharts 官网](https://echarts.apache.org/zh/index.html)
- [ECharts 配置手册](https://echarts.apache.org/zh/option.html)
- [图表组件在项目中的应用 ReportPlus 数据报表](https://www.ucharts.cn/v2/#/layout/info?id=1)
