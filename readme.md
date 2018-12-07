# nathan/pax [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 星系[最快的](#%E5%AE%83%E5%BF%AB%E5%90%97) JavaScript 捆绑器 」

[中文](./readme.md) | [english](https://github.com/nathan/pax)

---

## 校对 ✅

<!-- doc-templite START generated -->
<!-- repo = 'nathan/pax' -->
<!-- commit = '6d16b5867e943c9e9ef4e422f9d21b821a9b7f84' -->
<!-- time = '2018-09-01' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018-09-01 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/nathan/pax.svg
[commit]: https://github.com/nathan/pax/tree/6d16b5867e943c9e9ef4e422f9d21b821a9b7f84

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

# Pax

星系[最快的](#%E5%AE%83%E5%BF%AB%E5%90%97) JavaScript 捆绑器。完全支持 ECMAScript 模块语法(`import`/`export`)，除了 CommonJS 语法 `require(<string>)`。

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [我为什么需要它?](#%E6%88%91%E4%B8%BA%E4%BB%80%E4%B9%88%E9%9C%80%E8%A6%81%E5%AE%83)
- [我怎么得到它?](#%E6%88%91%E6%80%8E%E4%B9%88%E5%BE%97%E5%88%B0%E5%AE%83)
- [我该如何使用它?](#%E6%88%91%E8%AF%A5%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8%E5%AE%83)
- [它是否有源地图?](#%E5%AE%83%E6%98%AF%E5%90%A6%E6%9C%89%E6%BA%90%E5%9C%B0%E5%9B%BE)
- [模块?](#%E6%A8%A1%E5%9D%97)
- [有什么选项?](#%E6%9C%89%E4%BB%80%E4%B9%88%E9%80%89%E9%A1%B9)
- [它快吗?](#%E5%AE%83%E5%BF%AB%E5%90%97)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 我为什么需要它?

因为您的捆绑器是**太慢了**.

你知道这种感觉。你做了那个调整，点击<kbd>⌘S</kbd> <kbd>⌘Tab</kbd> <kbd>⌘R</kbd>,...**没有什么变化**.你得到旧版本。你让捆绑器挂了次。你等了几秒钟,再次<kbd>⌘R</kbd>，变化终于出现了。但为时已晚 -**你失去了行动力.**。那下一次可能会是个粉红色错误。因你用一个 z 拼写了 "menu"，而这些错误总在不经意间发生。

撤消，恢复，十个来回之后，事情看起来很好啦。现在是`git commit`的时候了，但是你**等待的时间，比花在工作上，要多得多**。这是你的捆绑器的错.

Pax 是一个捆绑器。但你永远不能打败它。为什么?

- 它是并行化的。它充分利用了您的 CPU。
- 这是最小的。它不会因您不需要的功能，而陷入困境。
- 它完全了解 JavaScript 以处理依赖项解析。它甚至不需要解析大部分源代码。

不要浪费时间，等待捆绑器，做它本该做的事情。在开发过程中使用 Pax,和**迭代出你心目中的内容**。当然，若您不关心运行时间有多长, 你完全可以使用超酷,神奇,慢速的最最亲爱的捆绑器，进行你的发布。

# 我怎么得到它?

```sh
cargo install pax
```

如果你没有`cargo`,安装它[https://rustup.rs](https://rustup.rs/).

# 我该如何使用它?

```js
// index.js:
const itt = require('itt');
const math = require('./math');
console.log(
  itt
    .range(10)
    .map(math.square)
    .join(' ')
);

// math.js:
exports.square = x => x * x;
```

```sh
> px index.js bundle.js
```

啪一声，写上`<script src="bundle.js">`，就准备好了。传递`-w`，可当您每更改文件时重建。

```sh
> px -w index.js bundle.js
 ready bundle.js in 1 ms
update bundle.js in 1 ms
...
```

# 它是否有源地图?

当然!

```sh
# bundle.js 和 bundle.js.map
> px index.js bundle.js

# bundle.js 内联地图
> px --map-inline index.js bundle.js

# bundle.js 没有地图
> px index.js >bundle.js
# 或
> px --no-map index.js bundle.js
```

# 模块?

这在技术上不是一个问题。但是,是的.

```js
// index.mjs
import itt from 'itt';
import {square, cube} from './math';

console.log(
  itt
    .range(10)
    .map(square)
    .join(' ')
);
console.log(
  itt
    .range(10)
    .map(cube)
    .join(' ')
);

// math.mjs
export const square = x => x * x,
  cube = x => x * x * x;
```

```
> px -e index.mjs bundle.js
```

如果由于某种原因，你需要你的模块始终为`.js`文件，可使用`-E`(`--es-syntax-everywhere`) 代替`-e`(`--es-syntax`).

# 有什么选项?

```
> px --help
pax v0.4.0

Usage:
    px [options] <input> [output]
    px [-h | --help]

Options:
    -i, --input <input>
         <input> 作为主模块.

    -o, --output <output>
        将 捆绑 <output> 和 source map 输出到 <output>.map.
        默认: '-' 为 stdout.

    -m, --map <map>
        输出 source map 到 <map>.

    -I, --map-inline
        输出 内联 source map , 用作: URI数据.

    -M, --no-map
        抑制 source map 输出，当为正常情况下.

    -w, --watch
        观察 <input> 和 它的 依赖.

    -W, --quiet-watch
        静静地看，就好了.
        覆盖 --watch.

    -e, --es-syntax
        支持ECMAScript 模块语法的 .mjs 文件:

            import itt from 'itt'
            export const greeting = 'Hello, world!'

        替代 CommonJS 的 require 语法:

            const itt = require('itt')
            exports.greeting = 'Hello, world!'

        .mjs (ESM) 文件 可以 import .js (CJS) 文件, 在这种情况下，命名空间对象有个`default`绑定，它反映了`module.exports`的值. CJS 文件 可以 require ESM 文件, 在这种情况下，结果对象是命名空间对象.

    -E, --es-syntax-everywhere
        覆盖 --es-syntax。  .js 文件 允许 ECMAScript 模块语法.
        CJS-格式 `require()` 也被允许调用。

    -x, --external <module1,module2,...>
        不要解析或包含名为 <module1>, <module2>, etc. 的模块;
        让他们在捆绑中作为 require('<module>') 引用. 指定一个路径，以替代 不做事的模块名。

    --external-core
        忽略 node.js的内置模块，像'events'之类的引用 和 让他们在捆绑中作为 require('<module>') 引用.

    -h, --help
        Print this message.

    -v, --version
        Print version information.
```

# 它快吗?

嗯...

是.

```sh
> time browserify index.js >browserify.js
real    0m0.225s
user    0m0.197s
sys     0m0.031s
> time node fuse-box.js
real    0m0.373s
user    0m0.324s
sys     0m0.051s
> time px index.js >bundle.js
real    0m0.010s
user    0m0.005s
sys     0m0.006s

# on a larger project
> time browserify src/main.js >browserify.js
real    0m2.385s
user    0m2.459s
sys     0m0.416s
> time px src/main.js >bundle.js
real    0m0.037s
user    0m0.071s
sys     0m0.019s

# want source maps?
> time browserify -d src/main.js -o bundle.js
real    0m3.142s
user    0m3.060s
sys     0m0.483s
> time px src/main.js bundle.js
real    0m0.046s
user    0m0.077s
sys     0m0.026s

# realtime!
> px -w examples/simple bundle.js
 ready bundle.js in 2 ms
update bundle.js in 2 ms
update bundle.js in 2 ms
update bundle.js in 1 ms
update bundle.js in 2 ms
update bundle.js in 1 ms
update bundle.js in 3 ms
^C
```
