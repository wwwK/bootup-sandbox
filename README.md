# bootup-sandbox

[![NPM version][npm-image]][npm-url] [![Build Status][ci-status-image]][ci-status-url] [![Coverage Status][coverage-status-image]][coverage-status-url] [![Known Vulnerabilities][vulnerabilities-status-image]][vulnerabilities-status-url] [![changelog][changelog-image]][changelog-url] [![license][license-image]][license-url]

[vulnerabilities-status-image]: https://snyk.io/test/npm/bootup-sandbox/badge.svg
[vulnerabilities-status-url]: https://snyk.io/test/npm/bootup-sandbox
[ci-status-image]: https://travis-ci.org/ufologist/bootup-sandbox.svg?branch=master
[ci-status-url]: https://travis-ci.org/ufologist/bootup-sandbox
[coverage-status-image]: https://coveralls.io/repos/github/ufologist/bootup-sandbox/badge.svg?branch=master
[coverage-status-url]: https://coveralls.io/github/ufologist/bootup-sandbox
[npm-image]: https://img.shields.io/npm/v/bootup-sandbox.svg?style=flat-square
[npm-url]: https://npmjs.org/package/bootup-sandbox
[license-image]: https://img.shields.io/github/license/ufologist/bootup-sandbox.svg
[license-url]: https://github.com/ufologist/bootup-sandbox/blob/master/LICENSE
[changelog-image]: https://img.shields.io/badge/CHANGE-LOG-blue.svg?style=flat-square
[changelog-url]: https://github.com/ufologist/bootup-sandbox/blob/master/CHANGELOG.md

[![npm-image](https://nodei.co/npm/bootup-sandbox.png?downloads=true&downloadRank=true&stars=true)](https://npmjs.com/package/bootup-sandbox)

在当前页面中启动一个沙箱环境, 让所有代码跑在沙箱中

## 原理

初衷: 在 PC 端页面中接入第三方的 IM 组件, 为了避免接入时可能存在的冲突

* 在当前页面中插入一个空的 `<iframe>` 元素
  * 作为独立的运行环境, 与当前页面隔离开(特别适合作为第三方的集成方案)
  * 避免与当前页面的 `CSS`/`JS` 冲突
* 将 `JS` 注入到 `<iframe>` 元素中执行
  * 动态创建 `<script>` 元素插入到 `<iframe>` 中

灵感来源[反击爬虫，前端工程师的脑洞可以有多大？](https://imweb.io/topic/595b7161d6ca6b4f0ac71f05), 感谢网易云音乐的 FE 们

> iframe异步加载式
>
> 例子：[网易云音乐](https://music.163.com/)
> 
> 网易云音乐页面一打开，html源码里几乎只有一个iframe，并且它的src是空白的：`about:blank`。接着js开始运行，把整个页面的框架异步塞到了iframe里面…

![music 163 com](https://user-images.githubusercontent.com/167221/54866079-b819fa00-4daa-11e9-803c-c5a22d170d03.png)

## Example

```javascript
import BootupSandbox from 'bootup-sandbox';

var sandbox = new BootupSandbox();
sandbox.injectScript('window.foo = "bar"', function() {
    console.log(sandbox.window.foo);
});
```

## APIDoc

* [ESDoc](https://doc.esdoc.org/github.com/ufologist/bootup-sandbox/)
* 兼容 IE9+
  * `Object.defineProperty`
  * `script.onload`
  * `postMessage`
  * `addEventListener`

## 其他思路

* [iframe-script](https://github.com/alexgorbatchev/iframe-script)
* [create-iframe](https://github.com/sethvincent/create-iframe)
* [iframe-sandbox](https://github.com/kumavis/iframe-sandbox)
* [jsonp-sandbox](https://github.com/aui/jsonp-sandbox)