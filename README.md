<center>检测字体加载状态以及后备方案的工具</center>


## 安装

```
npm install font-loader-observer
```

## 使用
1. `isSupportFontDisplay()` 检测浏览器是否支持 font-display CSS 属性。如果支持可以直接使用原生 CSS 控制字体加载模式

2. `watchFontLoaded(String fontFamily, Object options)` 如果不支持 font-display，则监听字体加载状态
 - `fontFamily`: 一个字符串，要检测的字体名称 
 - `options`: 可选项，支持参数：
    - `callback`: 字体加载完成的回调函数
    - `failed`: 字体加载失败的回调函数
    - `timeout`: 字体加载超时时间，单位秒。默认3000
    - `defaultFont`: 字体加载完成之前的默认字体
    - `referText`: 检测字体加载状态所用的字符串。默认是 "!\"\\#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[]^_`abcdefghijklmnopqrstuvwxyz{|}~"

```js
import {isSupportFontDisplay, watchFontLoaded} from 'font-loader-observer'

if (!isSupportFontDisplay()) {
    document.body.classList.add('font_loading');

    watchFontLoaded('test-font', {
        callback: function() {
            console.log('字体加载完成。Font loaded')
            document.body.classList.remove('font_loading');
        },
        defaultFont: 'sans-serif',
    })
} else {
    console.log('This environment supports the font-display property, and font-display can be used to set the font loading behavior directly')
}
```
[示例](./demo)

[github](https://github.com/xzhyj93/font-loader-observer) | 
[npm](https://www.npmjs.com/package/font-loader-observer) |
[掘金：原理介绍](https://juejin.im/post/5e93155c6fb9a03c546c38cd)