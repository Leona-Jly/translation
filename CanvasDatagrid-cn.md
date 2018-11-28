[TOC]

# canvas表格组件
[git地址](https://github.com/TonyGermaneri/canvas-datagrid)
[API文档地址](https://tonygermaneri.github.io/canvas-datagrid/docs/index.html#canvasDatagrid)

# 文档中文翻译 2018.11.23
## Readme
### canvas-datagrid
* 支持无限行和列，无需分页或加载等待；
* 快速绘画出数据，数据大小不会影响性能；
* 支持原生触摸设备（手机和平板）；
* 可扩展的样式、过滤器、格式化、尺寸调整、选择和排序；
* 丰富的事件、方法和属性API，写法和熟悉的W3C DOM一样；
* 支持Firefox, IE11, Edge, Safari and Chrome；
* 支持行及单元格内嵌表格；
* 支持列和行冻结；
* 支持右键层级菜单；
* 可自定义主题；
* W3C Web组件。所有框架皆可用；
* 可使用localStorage存储用户设定的样式、列尺寸、行尺寸、界面偏好和设置；
* 体积小，无依赖。

[文档](https://tonygermaneri.github.io/canvas-datagrid/docs/)
[教程](https://tonygermaneri.github.io/canvas-datagrid/docs/index.html#tutorials)
[支持](https://canvas-datagrid.slack.com/)
[主题生成器](https://tonygermaneri.github.io/canvas-datagrid/tutorials/styleBuilder.html)
[下载最新版(压缩版)](https://tonygermaneri.github.io/canvas-datagrid/dist/canvas-datagrid.js)
[测试](https://tonygermaneri.github.io/canvas-datagrid/test/tests.html)
[源码](https://github.com/TonyGermaneri/canvas-datagrid)
[最新测试覆盖率](https://tonygermaneri.github.io/canvas-datagrid/build/report/lcov-report/index.html)
[Coveralls测试](https://coveralls.io/github/TonyGermaneri/canvas-datagrid)

---

### Installation 安装
使用[npm](https://www.npmjs.com/package/canvas-datagrid)
```
npm install canvas-datagrid
```

在页面的script标签中引入源文件地址./dist/canvas-datagrid.js或者使用webpack。
```
<script src="dist/canvas-datagrid.js"></script>
```

或者，不需要下载安装，直接引用NPM CDN地址，如[unpkg.com](https://unpkg.com/)。
```
<script src="https://unpkg.com/canvas-datagrid"></script>
```

页面会引入全局函数方法canvasDatagrid及模块加载器。

---

### Getting started 开始
[使用webpack](https://tonygermaneri.github.io/canvas-datagrid/tutorials/amdDemo.html)，[不使用webpack](https://tonygermaneri.github.io/canvas-datagrid/tutorials/demo.html)或者使用[web组件](https://tonygermaneri.github.io/canvas-datagrid/tutorials/webcomponentDemo.html)。不管使用何种方式加载，方法canvasDatagrid都会在全局定义。

在能兼容Canvas-datagrid自定义标签的浏览器中，它是一个[web组件](https://www.webcomponents.org/element/TonyGermaneri/canvas-datagrid)，否则是一个<canvas>标签。

---

### Using pure JavaScript 只使用JS
```
var grid = canvasDatagrid();
document.body.appendChild(grid);
grid.data = [
    {col1: 'row 1 column 1', col2: 'row 1 column 2', col3: 'row 1 column 3'},
    {col1: 'row 2 column 1', col2: 'row 2 column 2', col3: 'row 2 column 3'}
];
```

---

### Using Web Component 使用web组件
```
<canvas-datagrid class="myGridStyle" data="data can go here too">[
    {"col1": "row 1 column 1", "col2": "row 1 column 2", "col3": "row 1 column 3"},
    {"col1": "row 2 column 1", "col2": "row 2 column 2", "col3": "row 2 column 3"}
]</canvas-datagrid>
```

或者

```
var grid = document.createElement('canvas-datagrid');
grid.data = [
    {"col1": "row 1 column 1", "col2": "row 1 column 2", "col3": "row 1 column 3"},
    {"col1": "row 2 column 1", "col2": "row 2 column 2", "col3": "row 2 column 3"}
];
```

---

### More Demos 更多例子
[使用Vue](https://tonygermaneri.github.io/canvas-datagrid/tutorials/vueExample.html)
[使用webpack3 AMD](https://tonygermaneri.github.io/canvas-datagrid/tutorials/amdDemo.html)
[使用React](https://tonygermaneri.github.io/canvas-datagrid/tutorials/reactExample.html)
[web组件例子](https://tonygermaneri.github.io/canvas-datagrid/tutorials/webcomponentDemo.html)
[XHR加载数据](https://tonygermaneri.github.io/canvas-datagrid/tutorials/demo.html)
[Sparkline图标例子](https://tonygermaneri.github.io/canvas-datagrid/tutorials/sparklineDemo.html)
[XHR加载分页数据例子Jeopardy Questions API](https://tonygermaneri.github.io/canvas-datagrid/tutorials/xhrPagingDemo.html)

注意XHR加载分页数据例子：多亏了[jservice](http://jservice.io/)提供的免费分页API。需要同意"加载不安全的脚本"或者相关的命令来允许HTTPS（github）向HTTP做出XHR请求（Jeopardy Questions API）。这没有什么不安全的。

---

### Building & Testing 打包和测试
安装development dependencies开发依赖。需要打包或测试。
```
npm install
```

打包生产版本和debug版本。
```
npm run build-all
```

打包生产版本。
```
npm run build-prd
```

打包debug版本。
```
npm run build-dev
```

在./lib中任一文件被修改时打包debug版本。
```
npm run build-watch
```

生成文档。
```
npm run build-docs
```

测试。注意：Headless tests（基于无界面化提供的命令行工具和api进行的前端测试手段）很有可能会因为不支持canvas像素检测而失败。使用VM测试或者用你自己的浏览器。
```
npm test
```

---

### Ways to create a grid 创建表格的方法
* document任意地方使用`<canvas-datagrid></canvas-datagrid>`标签创建web组件。
* 通过`var foo = document.createElement('canvas-datagrid')`创建web组件。
* webpack3通用模块加载器，添加其中一个加载器到代码中。例子：[https://tonygermaneri.github.io/canvas-datagrid/tutorials/amdDemo.html](https://tonygermaneri.github.io/canvas-datagrid/tutorials/amdDemo.html)。
* 执行全局方法`var foo = canvasDatagrid(<args>);`也可加载表格。例子：[https://tonygermaneri.github.io/canvas-datagrid/tutorials/demo.html](https://tonygermaneri.github.io/canvas-datagrid/tutorials/demo.html)。

若不使用web组件的方式加载表格，可以在使用模块加载器或全局方法实例化表格时，将`parentNode`属性值设为一个已有的canvas元素，以此来将表格挂载到该canvas元素中。使用`createElement`或标签方式实例化时该方法无效。

除了附加到已有的canvas上这个方法之外，表格会试图创建一个Shadow DOM元素并在其内部添加canvas。
* 对附加到已有canvas元素内的支持是实验性的。
* 在不支持自定义标签的浏览器中，`<canvas>`标签会代替`<canvas-datagrid>`标签。
* 在不支持Shadow DOM的浏览器中，不会生成shadow根元素。这种模式下，级联CSS会潜在性地破坏表格样式及行为。此时要注意CSS的使用。可能会影响到表格的行内修改和右键菜单。

---

### Setting Height and Width 设置高和宽
提高性能的最好方式就是限定canvas-datagrid元素的尺寸。
canvas-datagrid的默认设置是`grid.style.height: auto`和`grid.style.width: auto`。这意味着canvas-datagrid元素会根据包含的行和列来扩展高和宽。若有多行或多列，设置`grid.style.height`和`grid.style.width`为除`auto`以外的值。试试`100%`或`300px`。

当设置为auto以外的值时，canvas上会绘制一个虚拟滚动框来滚动列和行。

目前`max-width`, `max-height`, `min-width`和`min-height`还不支持，但已在计划之中。

---

### Setting and Getting Data 设置和获取数据
数据依据grid.dataType中定义的MIME类型解析器来设置。默认类型解析器是`application/x-canvas-datagrid`。这个解析器要求数据格式严格遵守表头要求（即：包含相同的属性或长度相同），格式为包含对象的数组或者包含数组的数组。

`application/x-canvas-datagrid`的例子
```
[
    {col1: 'row 1 column 1', col2: 'row 1 column 2', col3: 'row 1 column 3'},
    {col1: 'row 2 column 1', col2: 'row 2 column 2', col3: 'row 2 column 3'}
]
```

或

```
[
    ['row 1 column 1', 'row 1 column 2', 'row 1 column 3'],
    ['row 2 column 1', 'row 2 column 2', 'row 2 column 3']
]
```

无论数据如何设置，获取时一定是`application/x-canvas-datagrid`类型（一个包含对象的数组）。
更多关于使用和创建自定义解析器的信息参见[解析器](https://tonygermaneri.github.io/canvas-datagrid/docs/#parsers)。

下表列出了设置数据的方式以及默认使用的解析器。

| 方式 | 解析器 |
|-----|-----|
| 数据属性 | application/x-canvas-datagrid |
| web组件数据属性 | application/json+x-canvas-datagrid |
| web组件innerHTML属性 | application/json+x-canvas-datagrid |

有两个内置解析器。
application/x-canvas-datagrid (默认) application/json+x-canvas-datagrid。

注意：当通过web组件innerHTML属性来设置数据时，只有字符串类型的数据能被解析。

注意：向web组件传入字符串类型数据且`grid.dataType`被设为默认的`application/x-canvas-datagrid`时，解析器会转为`application/json+x-canvas-datagrid`来解析字符串数据。若`grid.dataType`之前被修改过，那么会使用修改后的解析器。

---

### Schema 表头
表头是可选项。表头是一个包含对象的数组。该文档会交替使用名词'表头'和'列'。没有提供表头时，会自动从数据data中生成一个，此时所有数据都将被假定为字符串。

注意：当数据data为二维数组时（包含数组的数组 vs. 包含对象的数组），列名会被设为A, B, C, D,...等。

每个表头对象有以下属性：

| 属性 | 描述 |
|-----|-----|
| name名称 | 列名。该属性用于匹配数据。唯一必填属性。 |
| type类型 | 列的数据类型。 |
| title标题 | 将显示于界面。若未设值，将使用name名称的值。 |
| width宽度 | 该列默认列宽，单位px。 |
| hidden隐藏 | 为true时，该列会被隐藏。 |
| filter过滤器 | 过滤器函数用于过滤列数据。若未提供函数，将由type类型来决定过滤器。 |
| formatter格式化 | 格式化函数用于格式化列数据。若未提供函数，将由type类型来决定格式化函数。 |
| defaultValue默认值 | 该列新行的默认值。可以是函数或者字符串。若使用函数，会提供参数`header`和`index`，必须返回新值。 |

表头例子：
```
[
    {
        name: 'col1'
    },
    {
        name: 'col2'
    },
    {
        name: 'col3'
    }
]
```

---

### Properties, Attributes, & Parameters 属性和参数
* properties, attributes属性和parameters参数代表了修改表格的值和行为的不同方式。properties属性可以直接在表格实例中修改。如：myGrid.someProperty = 'Some Value'；
* attributes属性可以在表格实例的attributes属性中修改。如：myGrid.attributes.someAttribute = 'Some Value'；
* attributes属性也可以在web组件的标签中设置。如：<canvas-datagrid someattribute="Some Value"></canvas-datagrid>；
* parameters参数是在实例时传入arguments参数对象的属性。如：var myGrid = canvasDatagrid({someAttribute: 'Some Value'});

---

### Web Component web组件
表格可以被实例化为一个web组件。
```
<canvas-datagrid></canvas-datagrid>
```

在标签之间增加JSON来设置数据data.
```
<canvas-datagrid>[
    {"col1": "row 1 column 1", "col2": "row 1 column 2", "col3": "row 1 column 3"},
    {"col1": "row 2 column 1", "col2": "row 2 column 2", "col3": "row 2 column 3"}
]</canvas-datagrid>
```

添加属性。使用HTML时，属性不分大小写。但若通过js来设置属性时，区分大小写。
```
<canvas-datagrid selectionmode='row'></canvas-datagrid>
```

自定义样式要增加前缀--cdg--且使用短横线连接，不要使用驼峰。例如，样式'gridBackgroundColor'写成'--cdg-grid-background-color'。class样式、css级联和行内样式对web组件都有效，就像其他HTML元素一样。

行内样式：
```
<canvas-datagrid style="--cdg-grid-background-color: lightblue;">[
    {"col1": "row 1 column 1", "col2": "row 1 column 2", "col3": "row 1 column 3"},
    {"col1": "row 2 column 1", "col2": "row 2 column 2", "col3": "row 2 column 3"}
]</canvas-datagrid>
```

class样式：
```
<style>
    .grid {
        --cdg-grid-background-color: lightblue;
    }
</style>
<canvas-datagrid class="grid">[
    {"col1": "row 1 column 1", "col2": "row 1 column 2", "col3": "row 1 column 3"},
    {"col1": "row 2 column 1", "col2": "row 2 column 2", "col3": "row 2 column 3"}
]</canvas-datagrid>
```

你仍可按你所想访问到表格，而且web组件实例的界面和通过模块加载器或全局函数方法创建的界面是一样的。web组件会有额外的从基础HTTPElement class中继承而来的属性。

更多关于web组件的详情参见[https://www.webcomponents.org/](https://www.webcomponents.org/)。
* 当在不支持自定义标签或css变量的浏览器中实例化表格时，class support不会生效。

---

### Parsers 解析器
包含了一系列MIME类型键名(MIME type keys)和解析函数值的对象。

| 参数 | 是否选填 | 描述 |
|-----|-----|-----|
| data数据 | false | 界面中的输入数据 |
| callback回调 | false | 回调函数。如下 |
| mineType mine类型 | true | MIME类型名称 |

callback回调

| 参数 | 是否选填 | 描述 |
|-----|-----|-----|
| data数据 | false | 输出数据 |

解析器例子：
```
grid.parsers['text/csv'] = function (data, callback) {
    var x, s = data.split('\n');
    for (x = 0; x < s.length; x += 1) {
        s[x] = s[x].split(',');
    }
    callback(s);
}
```

注意：这个方法用来解析CSV文件是非常糟糕的。这只是单纯作为一个解析器的例子。

---

### Sorters 排序器
包含了一系列排序函数的对象。

| 参数 | 描述 |
|-----|-----| 
| columnName列名 | 被排序的列名称 |
| direction方向| `asc`或`desc`表示升序或降序 |

排序器函数必须返回一个排序函数，该函数会被应用到[原生sort方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)中。

排序器例子：
```
grid.sorters.number = function (columnName, direction) {
    var asc = direction --- 'asc';
    return function (a, b) {
        if (asc) {
            return a[columnName] - b[columnName];
        }
        return b[columnName] - a[columnName];
    };
};
```

---

### Filters 过滤器
包含了一系列过滤器函数的对象。该对象的属性与`schema[].type`表头的类型相匹配。比如，若某列表头类型定义为`date`日期，则表格会查询名为`filters.date`的过滤器。若没有对应类型的过滤器，将会有警告提示，并且用string/RegExp过滤器代替。

```
filters.number = function (value, filterFor) {
    if (!filterFor) { return true; }
    return value --- filterFor;
};
```

---

### Formatters 格式化
包含了一系列格式化函数的对象。该对象的属性与`schema[].type`表头的类型相匹配。比如，若某列表头类型定义为`date`日期，则表格会查询名为`formatters.date`的格式化函数。若没有对应类型的格式化函数，将会有警告提示，并且用string格式化函数代替。

单元格格式化函数应该包含以下参数。
```
grid.formatters.date = function (e) { return new Date(e.cell.value).toISOString(); }
```

格式化函数必须返回一个字符串类型的值来展示在单元格中。

---

### Formatting using event listeners 使用事件监听来格式化
有两种方式可以不用修改data数据就可以格式化单元格的值。

第一种也是最快的方式，就是表格格式化函数。表格格式化函数能接收传入的值来进行格式化后绘制到表格。数据类型在[表头](https://tonygermaneri.github.io/canvas-datagrid/docs/#schema)中定义过了，所以可以选择性地传入来描述你的数据？？？。

这种方法略快是因为表格格式化函数运用了O(1)散列映射（O(1) hash map）。

下例中规定了格式化函数的类型为`date`日期。

```
grid.formatters.date = function (e) {
    return new Date(e.cell.value).toISOString();
};
```

格式化函数的返回值将会替换原值被显示在单元格中，但并不会修改原数据data。

第二种方法是`rendertext`事件。订阅`rendertext`事件监听可以拦截并修改[单元格](https://tonygermaneri.github.io/canvas-datagrid/docs/#canvasDatagrid.cell)值的绘制。

这种方法略慢是因为事件处理程序类运用了O(n)循环（O(n) loop）。

这种方法不依赖表头的值。该方法会覆盖`grid.formatters`表格格式化函数。

```
grid.addEventListener('rendertext', function (e) {
    if (e.cell.rowIndex > -1) {
        if (e.cell.header.name --- 'MyDateColumnName') {
            e.cell.formattedValue = new Date(e.cell.value).toISOString();
        }
    }
});
```

---

### Extending the visual appearance 扩展视觉外观
所有canvas的视觉元素的样式都依赖于style对象的值。通过style对象可以修改表格任意表格元素的尺寸和外观。

有两类样式，一类内置于DOM元素，如width宽度和margin外边距，另一类与canvas的绘制有关，这些在style部分中已列出。

下例修改了符合某个值的单元格的填充样式。

```
grid.addEventListener('rendercell', function (e) {
    if (e.cell.header.name --- 'MyStatusCell' && /blah/.test(e.cell.value)) {
        e.ctx.fillStyle = '#AEEDCF';
    }
});
```

---

### Drawing on the canvas 在canvas上绘制
跟常规HTML元素一样，可以通过事件处理函数扩展行为。可以通过事件处理函数修改已渲染的单元格内容。下面是一个在单元格中绘制图片的例子。

这个例子订阅了两个事件。`rendertext`事件阻止单元格内容的渲染...
```
grid.addEventListener('rendertext', function (e) {
    if (e.cell.rowIndex > -1) {
        if (e.cell.header.name --- 'MyImageColumnName') {
            e.cell.formattedValue = e.cell.value ? '' : 'No Image';
        }
    }
});
```

...以及`afterrendercell`事件在单元格背景和边框渲染完成后绘制图片。因为图片是异步加载的，所以需要订阅加载事件load来绘制出图片。
```
var imgs = {};
grid.addEventListener('afterrendercell', function (e) {
    var i, contextGrid = this;
    if (e.cell.header.name --- 'MyImageColumnName'
            && e.cell.value && e.cell.rowIndex > -1) {
        if (!imgs[e.cell.value]) {
            i = imgs[e.cell.value] = new Image();
            i.src = e.cell.value;
            i.onload = function () {
                i.targetHeight = e.cell.height;
                i.targetWidth = e.cell.height * (i.width / i.height);
                contextGrid.draw();
            };
            return;
        }
        i = imgs[e.cell.value];
        if (i.width !== 0) {
            e.ctx.drawImage(i, e.cell.x, e.cell.y, i.targetWidth, i.targetHeight);
        }
    }
});
```

---

### Supporting DOM elements 支持DOM元素
尽管表格本身是canvas，但仍有些表格元素是HTMLElements元素。
* 为了覆盖页面上的非canvas元素，右键菜单是一个`<div>`。
* 为了支持高级键盘命令、复制、粘贴及用户在此库外的自定义命令，编辑输入框/文本框是DOM元素。
* 一个隐藏的输入框被放置在页面可视区域之外来抓取键盘事件，并将其转换为表格命令，如光标导航。

通过订阅事件处理函数几乎可以自定义所有表格行为。大部分事件都提供`e.preventDefault();`方法来细粒度地操控表格行为。

如何通过事件处理函数来修改表格默认行为的例子在[教程](https://tonygermaneri.github.io/canvas-datagrid/docs/index.html#tutorials)部分。

---

### Cell Grids 单元格表格
单元格表格是单元格中canvas-datagrid的子实例。通过设置`canvas-datagrid`表头或者单元格`type`类型，单元格的值会被传入到单元格表格的data数据属性中。

可以通过在事件`beforerendercellgrid`或`beforecreatecellgrid`中调用`e.preventDefault();`来阻止单元格表格的绘制。可通过事件`beforecreatecellgrid`或`e.cellGridAttributes`来操控实例化单元格表格的参数。单元格表格的属性`cell.isGrid`为`true`。

---

### Notes 注意
* 整篇文档中，有几个名词会互换着使用。
* Canvas Datagrid会被简称为"grid"表格。
* column列和header头会互换使用。
* Node, HTMLElement, DOM, DOM element和element都是指HTML元素。
* Firing, raising, invoking和running都是指触发函数或事件。
* Binding绑定, subscribing订阅和listening监听都是指使用`<element>.addEventListener()`来订阅一个事件。
* Inner grid内部表格, child grid子表格, tree grid树形结构表格, cell grid单元格表格都是指表格嵌套。cell grids单元格表格是在一个单独单元格，而tree grids树形结构表格是在一整行。
* Drawing绘制和rendering渲染都是指使用基础方法把像素画到canvas上，通常是触发`canvasDatagrid.draw`方法。
* 这篇文档是自动生成的，所以可能有遗漏、失效链接和错误。有任何问题请发布在这里[https://github.com/TonyGermaneri/canvas-datagrid/issues](https://github.com/TonyGermaneri/canvas-datagrid/issues)。

---

## Parameters & Attributes 属性
## canvasDatagrid params参数
用法：
```
const grid = canvasDatagrid({
    parentNode: document.getElementById('canvasContainer'),
    schema: [
        {
            name: 'id',
        },
        ...
    ],
    data: [
        {
            id: 0,
        },
        ...
    ],
    allowColumnReordering: false,
    multiLine: true
})
```

* allowColumnReordering，默认值true。为true时，允许列重新排序。
* allowColumnResize，默认值true。为true时，允许用户调整列宽。
* allowColumnResizeFromCell，默认值false。为true时，允许用户通过拖拽单元格边框调整列宽。
* allowFreezingRows，默认值false。为true时，UI会显示一条可拖拽的分割线来冻结行。
* allowFreezingColumns，默认值false。为true时，UI会显示一条可拖拽的分割线来冻结列。
* allowMovingSelection，默认值true。为true时，用户可通过点击并拖拽选中区域的边框来移动并覆盖其他区域，原选中区域会变为空。（borderDragBehavior要设为'move'）
* allowRowHeaderResize，默认值true。为true时，允许用户调整表头列宽。
* allowRowReordering，默认值false。为true时，允许行重新排序。
* allowRowResize，默认值true。为true时，允许用户调整行高。
* allowRowResizeFromCell，默认值false。为true时，允许用户通过拖拽单元格边框来调整行高。
* allowSorting，默认值true。为true时，允许用户点击列表头来排序行。
* autoGenerateSchema，默认值false。为true时，每次设置data时都会自动从中提取出表头来覆盖之前的表头。
* autoResizeColumns，默认值false。为true时，会自动调整列宽来适应数据长度。警告！大于100k的数据会耗能巨大。
* borderDragBehavior，默认值'none'。拖拽边框时的行为。可设置为'resize', 'move', 或 'none'。设为'move'时，`allowMovingSelection`也要设为true。设为'resize'时，allowRowResizeFromCell 和/或 allowColumnResizeFromCell也要设为true。
* borderResizeZone，默认值10。在边框多少px范围内都是可以进行拖拽来调整大小的。？？？Number of pixels in total around a border that count as resize zones.
* cellGridAttributes，默认值无，要求值为对象格式。表格所使用的属性。子表格与树形结构表格不同。更多关于表格的信息参见`canvasDatagrid.data`属性。
* clearSettingsOptionText，默认值'Clear saved settings'。清除设置选项所显示的文字。
* columnHeaderClickBehavior，默认值'sort'。可设置为'sort', 'select', 或 'none'。设为'sort'时，单击列表头会进行升序/降序排列。设为'select'时，点击列表头会选中对应列。按住control/command或者shift可选中多列。
* columnSelectorHiddenText，默认值'&nbsp;&nbsp;&nbsp;'。文档有误，此处按源码来。列被隐藏时，点击右键Add/Remove columns选项中该列标题中左侧所显示的文字。
* columnSelectorText，默认值'Add/Remove columns'。右键菜单显示/隐藏列的文字显示。
* columnSelectorVisibleText，默认值'\u2713'。文档有误，此处按源码来。列显示时，点击右键Add/Remove columns显示/隐藏列选项中该列标题中左侧所显示的文字，默认为对勾符号√。
* contextHoverScrollAmount，默认值2。文档未写。鼠标hover在右键菜单滚动箭头上滚动一下移动的距离。
* contextHoverScrollRateMs，默认值5。文档未写。鼠标hover在右键菜单滚动箭头上滚动一下的毫秒数。
* copyHeadersOnSelectAll，默认值true。文档未写，无效？？？。为true时，选中所有复制时也复制表头。
* copyText，默认值'Copy'。当复制可用时，显示在右键菜单上的文字。
* data，默认值[]。设置data，详见canvasDatagrid.data。
* debug，默认值false。设为true时，debug信息会显示在表格顶部。
* editable，默认值true。设为true时，单元格可编辑。设为false时，单元格只读。
* ellipsisText，默认值'...'。被截断的文本所显示的省略文字。
* filterOptionText，默认值'Filter %s'。文档未写。右键菜单中过滤的显示文本。
* filterTextPrefix，默认值'(filtered) '。文档未写。过滤文字前缀。
* filters，默认值{}。设置过滤器的值。详见canvasDatagrid.filters。
* formatters，默认值{}。设置格式化的值，详见canvasDatagrid.formatters。
* globalRowResize，默认值false。为true时，调整一行的高度将会应用到所有行。
* hideColumnText，默认值'Hide %s'。右键菜单中隐藏列的显示文本。
* maxAutoCompleteItems，默认值200。右键菜单中过滤项的下拉选项框最多显示几项，0表示1项，以此类推。文档未写。
* maxPixelRatio，默认值1.5。最大像素比。高DPI设备的最大像素比。高DPI设备会引起性能迟缓，这会影响表格渲染。标准分辨率（比如1920×1080）像素比为1:1，更高的分辨率会有更高的像素比（如Retina设备像素比为2:1）。数字越高对应分辨率越高，数字越低分辨率越低。把值设为小于1的数可能会很有趣哦，我反正是没干过这事。
* multiLine，默认值false。设为true时，单元格编辑框为textarea文本框，false时为input输入框。详见tutorial--Use-a-textarea-to-edit-cells-instead-of-an-input。
* name，默认值''。可选项，可在浏览器本地存储中存入列高，行宽等。每个表格的name必须是唯一的。
* pageUpDownOverlap，默认值1。每次使用键盘pageup/pagedown翻页时盈余的行数。
* parentNode，默认值无。表格的父级HTML元素。这个块级元素必须有高度，canvas-datagrid会自己添加canvas并适应该元素的大小。window.resize时间和DOM变化时，canvas会重新调整大小。若使用时它没有改变大小，则需要手动触发canvas-datagrid.resize()方法。若使用的不是web component方式，父级元素可以是canvas。
* parsers，默认值{}。设置parsers中选中的值。详见canvasDatagrid.parsers。
* pasteText，默认值'Paste'。当粘贴可用时，显示在右键菜单上的文字。
* persistantSelectionMode，默认值false。为true时，选中区域时会表现得像是一直按住command/control一样。
* removeFilterOptionText，默认值'Remove filter on %s'。文档未写。移除过滤选项显示的值。
* reorderDeadZone，默认值3。Number of pixels needed to move before column reordering occurs.在执行列排序前需要移动的px值。？？？
* resizeScrollZone，默认值20。文档未写。调整滚动区域大小。
* rowGrabZoneSize，默认值5。文档未写。行的拖动区域大小。
* saveAppearance，默认值true。为true时，并且属性name也已设置值时，列和行的大小会被保存在浏览器本地存储localStore里。
* schema，默认值[]。设置表头，详见canvasDatagrid.schema。
* scrollAnimationPPSThreshold，默认值0.75。在触摸释放时的触摸动画发生之前，必须达到每秒多少个点。？？？
* scrollPointerLock，默认值false。为true时，点击滚动框进行滚动时，鼠标光标会消失，来防止其离开表格的可视区域。
* scrollRepeatRate，默认值75。文档未写。滚动重复率。
* selectionFollowsActiveCell，默认值false。为true时，用键盘移动active单元格时会同时移动选中区域。
* selectionHandleBehavior，默认值'none'。若设为除'none'以外的值，则会在pc端表格的active单元格右下角显示一个小方块。目前无功能，将来的版本会用到。
* selectionMode，默认值'cell'。可设置为'cell'或'row'。该设置规定了点击一个单元格时是选中单元格还是整行。
* selectionScrollIncrement，默认值20。文档未写。选中区域滚动增量。
* selectionScrollZone，默认值20。文档未写。选中区域滚动区域。
* showClearSettingsOption，默认值true。为true时，右键菜单显示'清除已保存的设置'选项。
* showColumnHeaders，默认值true。为true时，显示列表头。
* showColumnSelector，默认值true。为true时，右键菜单显示'显示/隐藏'选项。
* showCopy，默认值false。为true时，当复制可用时，会显示在右键菜单。
* showFilter，默认值true。为true时，右键菜单显示'过滤'选项。
* showNewRow，默认值false。文档默认值为true，源码默认值为false。为true时，会在表格最下方显示新行，data set. schema[].defaultValue可以设置每个单元格的默认值。默认值可以是string或者function。若是function，header和index会作为参数传入。function最后return的值就是新单元格的值。详见canvasDatagrid.header.defaultValue。
* showOrderByOption，默认值true。为true时，右键菜单显示'排序'选项。
* showOrderByOptionTextAsc，默认值'Order by %s ascending'。右键菜单升序排序所显示的文字。
* showOrderByOptionTextDesc，默认值'Order by %s descending'。右键菜单升序排序所显示的文字。
* showPaste，默认值false。为true时，当粘贴可用时，会显示在右键菜单。
* showPerformance，默认值false。为true时，会渲染一个显示性能的表格。
* showRowHeaders，默认值true。为true时，显示行表头。
* showRowNumbers，默认值true。为true时，行表头会显示序列数。
* snapToRow，默认值false。为true时，scrolling snaps to the top row.？？？
* sorters，默认值{}。设置排序的值。详见canvasDatagrid.sorters。
* style，默认值{}。设置样式。
* touchContextMenuTimeMs，默认值800。在触摸盲区触摸多少毫秒数会出现右键。
* touchDeadZone，默认值3。触摸必须在attributes.touchSelectTimeMs设置的时间内移动多少px才能被认定为滚动操作，而不是选择操作。
* touchEasingMethod，默认值'easeOutQuad'。触摸时的动画淡出方式。可选值有easeOutQuad, easeOutCubic, easeOutQuart, easeOutQuint。
* touchReleaseAcceleration，默认值1000。触摸释放加速度。How many times the detected pixel per inch touch swipe is multiplied on release. Higher values mean more greater touch release movement.？？？
* touchReleaseAnimationDurationMs，默认值2000。触摸释放后的淡出动画的持续时间。
* touchScrollZone，默认值20。文档默认值为30，源码默认值为20。When touching, the scroll element hit boxes are increased by this number of pixels for easier touching.？？？
* touchSelectHandleZone，默认值20。触摸选中处理的半径px值。
* touchZoomMax，默认值1.75。放大的最大倍数。
* touchZoomMin，默认值0.5。缩小的最小值。
* touchZoomSensitivity，默认值0.005。触摸缩放敏感度。
* maxPixelRatio，默认值2。文档未写。最大的px比例。
* tree，默认值false。为true时，每行都会绘制一个箭头，点击时会触发canvasDatagrid#event:expandtree事件，并生成一个内部表格。详见tutorial--Allow-users-to-open-trees。
* treeGridAttributes，默认值无，要求值为对象。树形结构表格的属性。子表格不同于单元格表格。详见canvasDatagrid.data。
* treeHorizontalScroll，默认值false。为true时，展开的子表格会横向滚动。为false时，横向滚动时子表格保持不动。这不会影响垂直滚动。

---

## Properties属性
用法：
```
const grid = canvasDatagrid({
    parentNode: document.getElementById('canvasContainer'),
    schema: [...],
    data: [...]
})
console.log(grid.activeCell) // {columnIndex: 0, rowIndex: 0}
grid.columnOrder = [2,1,0]
```

* activeCell，类型object。获取被选中的单元格对象，内容为rowIndex和columnIndex。
* attributes，类型object。包含了attribute部分列出的属性。这些属性可以在实例化时被修改。完整版文档参见canvasDatagrid.params部分。
* canvas，类型object。绘制当前表格的canvas元素。
* changes，类型array。自最后一次data数据加载后对表格的增加和修改。The data property will change with changes as well, but this is a convince list of all the changes in one spot. data属性也会受到修改的影响而改变，但这是某个时间点的所有修改的清单？？？。调用clearChangeLog会清除该数组。
* childGrids，类型boolean。该表格中由内部唯一的行id组织起来的子表格。
* columnOrder，类型array。获取列的下标数组。这能在不改动data的情况下修改表头的外观。数组的顺序规定了列的顺序，如[0,1,2]是正常的顺序，[2,1,0]则是反向的顺序。数组长度必须等于或大于列的长度。可赋值。
* controlInput，类型object。键盘控制的input输入框。任何在表格上的点击就会使该input获得焦点。该input被隐藏在浏览器窗口的左上角。
* currentCell，类型canvasDatagrid.cell。鼠标最后移过的单元格。
* data，类型canvasDatagrid.data。这是表格中设置data的方法。data必须是一个包含对象的数组，且和表头一一对应。data的值可以是任何原始类型。但是，若一个单元格的值是另一个data数组，则会在该单元格生成一个内部表格。这个'单元格表格'和'树状结构表格'（行表头会有箭头可以展开收起）不一样，可以使用cellGridAttributes属性来获取属性和样式。详见canvasDatagrid.data。
* dragMode，类型string。表示当前鼠标调整大小时的指针样式。可设置为ns-resize, ew-resize, pointer, 或inherit。
* filters，类型canvasDatagrid.filter。包含了一系列用来过滤data的过滤器的列表。该对象中的属性与schema[].type相匹配。比如，某列表头类型type为date，那么表格就会查找名为filters.date的过滤器。若找不到该类型对应的过滤器，会有警告提示，并使用string/RegExp来代替。
* formatters，类型canvasDatagrid.formatter。包含了对显示文字格式化的函数。该对象中的属性与schema[].type相匹配。比如，某列表头类型type为date，那么表格就会查找名为formatters.date的格式化函数。若找不到该类型对应的格式化函数，会有警告提示，并使用string类型的格式化函数来代替。格式化函数必须返回一个string值来显示在单元格里。详见canvasDatagrid.formatters。
* frozenColumn，类型number。被冻结的列的最大下标。若设为比可见列数更大的值会导致range error错误。
* frozenRow，类型number。被冻结的行的最大下标。若设为比可见行数更大的值会导致range error错误。
* hasFocus，类型boolean。为true时，该表格已被聚焦。
* height，类型number。表格的高度。
* input，类型object。指编辑时弹出的输入框元素。未在编辑时则为undefined。编辑时，该DOM元素会覆盖在被编辑的单元格上，并完全可见。
* isChildGrid，类型boolean。为true时，该表格是另一个表格的子表格。即，它是另一个表格的树状结构表格或单元格表格。
* offsetLeft，类型number。表格offset left距离左侧的值。
* offsetTop，类型number。表格offset top距离顶部的值。
* openChildren，文档类型为boolean，实际类型object或array？？？。根据内部唯一的行id所展开的子表格的清单。
* orderBy，类型string。最后一次按列排序时，那列的名称name。可将其值设为任一列名来改变其排序，排序方式按照数据类型所定义的来。订阅beforesortcolumn事件并执行e.preventDefault能够修改该属性及表格的图形外观（每列都会被绘制排序箭头），无需调用客户端的排序方法。该方法在想要使用客户端data排序的时候非常有用。可赋值。
* orderDirection，类型string。获取或设置排序方向，值可以为asc升序或desc降序。订阅beforesortcolumn事件并执行e.preventDefault能够修改该属性及表格的图形外观（每列都会被绘制排序箭头），无需调用客户端的排序方法。该方法在想要使用客户端data排序的时候非常有用。可赋值。
* parentGrid，类型canvasDatagrid。若当前表格为子表格，该属性为该表格的父级表格。
* parentNode，类型HTMLElement。canvas的父节点，通常是shadow DOM的父元素。
* rowOrder，类型array。获取或设置行的排序。这能在不改动data的情况下修改数据的外观。数组的顺序规定了行的顺序，如[0,1,2]是正常的顺序，[2,1,0]则是反向的顺序。数组长度必须等于或大于行的长度。可赋值。
* schema，类型canvasDatagrid.schema。表头是非必填项。表头是一组包含{canvasDatagrid.header}对象的数组。schema没有填的话会自动从data中生成，这时候data都将被假定为string类型。详见canvasDatagrid.schema。
* scrollHeight，类型number。能够被垂直滚动的总px值。
* scrollIndexRect，类型object。描述虚拟canvas视窗的列和行下标的rect矩形对象。当你只想对可见的单元格做操作的话，这个属性可以检测可见单元格的范围。
* scrollLeft，类型number。横向滚动条当前位置距离左侧的px值。
* scrollPixelRect，类型object。描述虚拟canvas视窗的px值的rect矩形对象。
* scrollTop，类型number。竖向滚动条当前位置距离顶部的px值。
* scrollWidth，类型number。能够被横向滚动的总px值。
* selectedCells，类型array。描述用户选中的单元格的不规则数组jagged array。注意这是个不规则数组，所以有些下标是null。除掉null之外的该数据就跟传入的data一样，只不过只有用户选中的那些单元格。所以若用户选中10行10列那个单元格，数组会有9个null值。
* selectedRows，类型array。选中的行。和data属性一样，但是只有用户选中单元格的行的对象。一行中选中了任意单元格，该数组都会列出整一行对象。bug：实际只列出被选中的单元格信息。
* selectionBounds，类型rect。当前选择的rect矩形对象。
* selections，类型array。选中单元格的矩形数组。
* shadowRoot，类型HTMLElement。shadow根元素。
* sizes，类型object。由sizes.columns和sizes.rows组成的变化对象，能够控制列和行的大小。若不能获取到行和列下标，则会使用默认样式。
* sorters，类型canvasDatagrid.sorter。包含了一系列排序函数的对象集。详见{@tutorial sorters}。
* style，类型canvasDatagrid.style。包含了style章节列出来的属性。改变样式会自动执行draw方法。
* visibleCells，类型array。被绘制的表格数据集合。
* visibleRowHeights，类型array。可见行的高度集合。
* visibleRows，类型array。可见行的下标集合。
* width，类型number。表格的宽。

---

## methods方法
用法：
```
const grid = canvasDatagrid({
    parentNode: document.getElementById('canvasContainer'),
    schema: [
        {
            name: 'id',
            type: 'customNumber',
        },
        ...
    ],
    data: [
        {
            id: 0,
        },
        ...
    ]
})
grid.addColumn({...})
grid.filters.customNumber = function (value, filterFor) {
    if (!filterFor) { return true; }
    console.log('customNumber filter executed');
    return value --- filterFor;
};
```

* addColumn：增加列头。增加新的一列至表头。参数为表头对象。
* addEventListener：增加监听事件至已有事件。第一个参数为需要监听的事件名称，string，第二个参数为方法。
* addRow：增加行。参数为数据对象。
* appendTo：添加到。添加表格到另一个元素。没有实现。
* applyComponentStyle：添加组件样式。将计算好的css样式应用到表格上。在某些浏览器上，对附加样式表执行修改指令不会自动更新组件样式。此时需要执行该方法。
* beginEditAt：在x列y行开始编辑。第一个参数x为列下标，number，第二个参数y为行下标，number。
* blur：从表格上失去焦点。
* clearChangeLog：清除用于记录数据修改的grid.changes文件。该方法不会撤销之前的修改，也不会修改数据，只是单纯地删除grid.changes文件。该文件通过数组的方式记录了之前的数据修改。
* collapseTree：折叠树形结构。通过行下标折叠树形结构。参数index为需要折叠的行下标，number。
* deleteColumn：删除列。删除指定表头下标的列。参数index为需要删除的列下标，number。
* deleteRow：删除行。删除指定下标的行。参数index为需要删除的行下标，number。
* dispatchEvent：派发事件。调用指定事件，并传入一个event对象至事件订阅者。第一个参数e为event对象，第二个参数ev为需要派发的事件名称。
* dispose：释放。释放表格资源，删除表格元素。
* draw：绘制。重新绘制表格。不管对表格做什么修改，这是刷新数据唯一需要被调用的方法。
* endEdit：终止编辑。参数abort为boolean值，true表示终止编辑，不将编辑内容赋值到源数据中。
* expandTree：展开树形结构。根据行下标展开树形结构。参数index表示需要展开的行下标，number。
* filter：过滤函数。函数中，当值需要被保留时返回true，需被过滤掉时返回false。必须定义在canvasDatagrid.filters中，且匹配canvasDatagrid.headers在canvasDatagrid.schema中的一个类型，具体意思见开头用法。第一个参数filterFor为需要被过滤的值，string，第二个参数value为当前被循环到的值，string。可在表头中定义。
* findColumnMaxTextLength：找到列中最长值的宽度。返回指定列中最长的值的宽度。参数name为需要计算值宽度的列的名称，string。
* findColumnScrollLeft：列向左滚动的距离。返回指定列的左滚动px值，number。
* findRowScrollTop：行向下滚动的距离。返回指定行的垂直滚动px值，number。
* fitColumnToValues：列宽适应列值。调整列的宽度来适应列中最长的值。不传值则调整所有列宽。警告，在数据很大时可能会影响速度（在i7中，1兆数据会延迟3到5秒）。参数name表示需要被调整宽度的列名称，string。bug：不传参报错。
* focus：聚焦至表格。
* forEachSelectedCell：循环选中的单元格。对每个选中的单元格执行指定方法。第一个参数expandToRow为true的时候，将执行对象扩展到整行，第二个参数fn为执行的回调函数，参数为data，rowIndex，columnName。
* formatter：格式化函数。必须定义在canvasDatagrid.formatters，且匹配canvasDatagrid.headers在canvasDatagrid.schema中的一个类型。参数e为格式化event对象，其中e.cell为需要被格式化的单元格。
* getCellAt：获取单元格。获取指定像素坐标轴x、y位置的单元格。该方法结合了绘制和事件，非常复杂，是组件的核心。
* getColumnWidth：获取指定下标的列宽。参数columnIndex为列下标，number。
* getDataTypes：获取当前注册的MIME类型数组。
* getHeaderByName：获取指定名称的表头。返回指定名称的schema表头对象。参数name为名称。
* getHeaderWidth：获取表头宽度。获取表头总列宽。bug：grid上找不到该方法？？？
* getRowHeight：获取行高。获取指定下标行的高度。参数rowIndex为行下标，number。bug：grid上找不到该方法？？？
* getSchemaFromData：获取表头数据。返回根据源数据自动计算出来的表头数据。
* getSelectionBounds：获取选中区域的范围。bug：grid上找不到该方法？？？
* getVisibleCellByIndex：获取指定下标的单元格对象。获取指定列下标和行下标的单元格。第一个参数为列下标，number，第二个参数为行下标，number。
* gotoCell：滚动到指定列下标x和行下标y的单元格。若同时指定行下标和列下标，方法会根据目标单元格的宽高进行额外的计算。若只定义其中一个下标，则计算会简单点。第一个参数x为列下标，number，第二个参数y为行下标，number，第三个参数offsetX，可选，为距离最左边框（不包括头）的百分比。默认为0，表示单元格将会滚动到最左边。有效值为0到1。1表示左边，0表示右边，0.5表示中间。第四个参数offsetY，可选，为距离顶部边框（不包括头）的百分比。默认为0，表示单元格将会滚动到顶部。有效值为0到1。1表示底部，0表示顶部，0.5表示中间。无效？？？
* gotoRow：滚动到指定下标行。参数y表示需要滚动到的行下标，number。无效？？？
* insertColumn：插入列。在指定的表头下标前插入一列。第一个参数c为需要插入的列数据，第二个参数index表示需要在哪一列下标前插入，number。
* insertRow：插入行。在指定的行下标前插入一行。第一个参数d为需要插入的行数据，第二个参数index表示需要在哪一行下标前插入，number。
* integerToAlpha：将整数序号转换为字母A-ZZZZZ...。参数n为需要转换的数字。只是一个方法，不会对改变表格。
* isCellVisible：检查一个单元格当前是否可见，返回布尔值。第一个参数columnIndex为需要检查的单元格的列下标，number，第二个参数rowIndex为行下标，number。
* isColumnSelected：检查列是否被选中。若整列被选中返回true。参数columnIndex为需要检查的列下标，number。bug：grid上找不到该方法？？？
* isColumnVisible：检查指定列是否可见。参数columnIndex为列下标，number。
* isRowVisible：检查指定行是否可见。参数rowIndex为行下标，number。
* moveSelection：移动选中区域。将当前选中区域移动到某个相对于当前区域的位置。注意：这个方法不会移动选中的数据，只会移动被选中的区域范围。第一个参数offsetX为列的相对距离，number，第二个参数offsetY为行的相对距离，number。
* moveTo：移动到。将指定区域的数据移动到表格的另一个位置。将数据移出表头最大下标将会截断数据。第一个参数sel为选中区域的行列坐标2D数组，canvasDatagrid.selections符合参数数组格式，可以在此使用，array。第二个参数x为移动终点位置的列下标，第三个参数y为移动终点位置的行下标。
* order：给data排序。第一个参数columnName为需要被排序的列名称，string。第二个参数direction为排序方式，asc为升序，desc为降序，string。第三个参数dontSetStorageData可选，表示不存储当前的设置，Boolean。第四个参数sortFunction可选，若传入方法会覆盖默认排序方式，function。
* removeEventListener：移除事件监听。将指定的监听函数移出事件。移除的函数名必须是绑定的实际函数名称（应该是说需要函数的地址指向变量，不能用匿名函数？？？）。第一个参数ev为需要解除的事件名称，string，第二个参数为该事件发生时触发的函数，function。
* resetColumnWidths：清除所有用户或者api对列宽的修改，恢复到表头设置的或默认样式的列宽。
* scrollIntoView：滚动到视野范围内。将指定的单元格滚动到视野范围内。第一个参数x为列下标，number，第二个参数y为行下标，number，第三个参数offsetX，可选，为距离最左边框（不包括头）的百分比。默认为0，表示单元格将会滚动到最左边。有效值为0到1。1表示左边，0表示右边，0.5表示中间。第四个参数offsetY，可选，为距离顶部边框（不包括头）的百分比。默认为0，表示单元格将会滚动到顶部。有效值为0到1。1表示底部，0表示顶部，0.5表示中间。无效？？？
* selectAll：选中所有可见单元格，不包括表头。参数dontDraw表示修改选中区域时是否阻止绘制方法执行，Boolean。（true则不会选中，false会选中所有可见单元格。）
* selectArea：选择表格某个区域。参数bounds为rect对象，表示选中的值。rect格式为 { left: 1, top: 1, right: 5, bottom: 5 }。
* selectColumn：选择一列。第一个参数columnIndex为需要选择的列下标，number。第二个参数toggleSelectMode为true时，在你点击列时会表现出你按住ctrl/command时的状态，Boolean。第三个参数shift为true时，当你点击列时会表现出你按住shift时的状态，Boolean。第四个参数supressSelectionchangedEvent为true时，不会触发selectionchanged监听事件，Boolean。
* selectNone：移除选择。参数dontDraw表示修改选中区域时是否阻止绘制方法执行，Boolean。
* selectRow：选择一行。第一个参数rowIndex为需要选择的行下标，number。第二个参数ctrl为true时，在你点击列时会表现出你按住ctrl/command时的状态，Boolean。第三个参数shift为true时，当你点击列时会表现出你按住shift时的状态，Boolean。第四个参数supressSelectionchangedEvent为true时，不会触发selectionchanged监听事件，Boolean。
* setActiveCell：选中指定单元格。需要重绘。第一个参数x为列下标，number，第二个参数y为行下标，number。
* setColumnWidth：设置列宽。第一个参数colIndex为列下标，number，第二个参数width为列宽，number。
* setFilter：设置过滤的值。第一个参数column为需要过滤的列名称，string，第二个参数value为过滤的文本，string。
* setRowHeight：设置指定行的高度。第一个参数height为高度，number，第二个参数rowIndex为行下标，number。
* sorter：排序函数。必须定义在canvasDatagrid.sorters中，且匹配canvasDatagrid.headers在canvasDatagrid.schema中的一个类型。第一个参数columnName为需要排序的列名称。第二个参数direction为排序方向，asc升序，desc降序。
* toggleTree：切换指定行下标的树形结构的展开收起。参数index为行下标。

---

## events事件
用法：
```
const grid = canvasDatagrid({
    parentNode: document.getElementById('canvasContainer'),
    schema: [...],
    data: [...]
})
grid.addEventListener('afterrendercell', function (e) {
    ...
});
```

* afterrendercell：单元格被绘制之后。此事件可用来在单元格内绘制内容。可在canvas上绘制内容，也可改变canvas的上下文。
* appendeditinput：插入编辑输入框。当编辑框插入页面的时候触发。可在此事件中使用e.preventDefault来阻止插入，然后在任何地方插入输入框。输入框默认绝对定位在原cell上。所有的style都是行内样式。你可以改变任何东西，比如大小、样式、父元素。如果使用了e.preventDefault，确保你在其他地方添加了输入框，不然你无法使用它。当编辑完成时，输入框自己会删除。
* attributechanged：属性被改变时。
* beforebeginedit：在编辑框生成之前。可通过e.preventDefault来终止编辑框的生成。
* beforecreatecellgrid：在单元格创建之前。可通过e.preventDefault来终止单元格的创建。也可在此事件中修改单元格表格实例化参数。每个表格创建时只触发一次。
* beforeendedit：在编辑结束前，可在此时验证输入内容。e.preventDefault可以阻止编辑生效，不会覆盖原数组对象。老数据e.oldValue，新数据e.newValue。bug：e.preventDefault会阻止输入框内容覆盖源数据，但是不会使当前编辑框消失。解决：暂时想到document.querySelectorAll('input').forEach(e => e.remove())。
* beforerendercell：在单元格绘制之前。e.preventDefault会阻止单元格的绘制。bug：使用e.preventDefault后，单元格虽未被绘制，但双击时仍可编辑且可覆盖原数据。需要处理。
* beforerendercellgrid：在单元格表格绘制之前。可通过e.preventDefault来终止单元格的绘制。表格绘制时只触发一次。
* beforesortcolumn：在列排序之前。e.preventDefault会阻止排序。和gird.orderBy、grid.orderDirection组合使用，可使用原始的箭头排序来完成服务器端排序。bug：其他列排序多次后，点击阻止排序的那列会影响到旁边列的排序箭头，但不会改变其排序。
* beforetouchmove：触摸移动之前。可以在此事件中阻止touchmove的默认行为。
* beginedit：编辑文本框或输入框被创建之后。
* beginfreezemove：开始移动冻结分割线时。e.preventDefault可以阻止移动。
* beginmove：开始移动选中区域时。e.preventDefault可以阻止移动。
* cellmouseout：鼠标移出单元格时。
* cellmouseover：鼠标移入单元格时。
* click：点击单元格时。
* collapsetree：折叠已打开的树形结构时。
* columnmouseout：鼠标移出一列时。
* columnmouseover：鼠标移入一列时。
* contextmenu：点击鼠标右键唤出菜单时。可修改菜单数组列表来改变右键菜单。可以增加右键菜单，但一定要遵守canvasDatagrid.contextMenuItem。若删除右键数组列表，则点击右键不会出现菜单。e.preventDefault同样可以阻止右键菜单出现。
* copy：执行复制操作时。
* datachanged：数据被改变时。
* dblclick：双击单元格时。e.preventDefault可阻止默认事件。注意，双击事件需要2次mousedown，2次mouseup和2次点击？？？
* endedit：结束编辑时。可在此事件中丢弃输入的内容，保留原来的老数据，或者在数据被覆盖之前修改data的值？？？
* endfreezemove：松开冻结分割线时。e.preventDefault可以阻止松开。
* endmove：结束移动选中区域时。e.preventDefault可以阻止结束。
* expandtree：点击左侧箭头打开树形结构。点击箭头时，生成新的嵌套表格。表格、行数据和行下标都会传给监听事件，可用来操作内部表格。树结构被折叠时，表格只是被隐藏，但若树结构不展开，表格不会被创建。
* formattext：文本将要被格式化时。可通过e.preventDefault来阻止默认的格式化函数和换行。可以提升长值（如不要求格式化的数字列表）的性能或者用自己的格式化函数替换默认的。阻止默认时，要将e.cell.text属性设为像这样的数组{ lines: [{value: "line 1" }, {value: "line 2" }] }。每一个数组成员都应该适应单元格的宽度，lines的总数应该适应单元格的高度。
* freezemoving：拖动冻结分割线时。e.preventDefault可阻止拖动。
* keydown：键盘落下时。e.preventDefault可阻止默认事件。
* keypress：按住键盘时。e.preventDefault可阻止默认事件。
* keyup：松开键盘时。e.preventDefault可阻止默认事件。
* mousedown：按下鼠标时。e.preventDefault可阻止默认事件。
* mousemove：移动鼠标时。
* mouseup：松开鼠标时。e.preventDefault可阻止默认事件。
* mousewheel：鼠标滚动滚轮时。
* moving：鼠标移动选中区域时。e.preventDefault可阻止默认事件。
* rendercell：单元格绘制完成时。可在此事件中改变颜色、大小、宽高、canvas对象上下文。在canvas上的绘制操作可能会被单元格的绘制覆盖。字体颜色需在rendertext中修改。
* rendercellgrid：表格绘制调用绘制方法之后。可改变数据。每个子表格只触发一次。
* renderorderbyarrow：绘制排序箭头时。这是唯一一个可以替换排序箭头图标的事件。e.preventDefault可阻止箭头绘制。
* rendertext：绘制单元格文字时。可在此事件中改变字体颜色。改变cell.formattedValue的值可修改单元格最终呈现的值。记住，文字超出单元格的部分仍会变为省略号。在此事件中，不能改变单元格的宽高，若想改，请在rendercell中改。
* rendertreearrow：绘制树形结构箭头。这是唯一一个可以替换树形结构箭头图标的事件。e.preventDefault可阻止树形结构箭头绘制。
* reorder：用户结束列或行的重新排序时。e.preventDefault可阻止列的重新排序。
* reordering：用户进行列或行的重新排序时。e.preventDefault可阻止列开始排序。
* resize：表格尺寸被调节时。
* resizecolumn：列尺寸将要被调节时。e.preventDefault可将当前跳转的尺寸失效。
* rowmouseout：鼠标移出一行时。
* rowmouseover：鼠标移入一行时。
* schemachanged：表头数据被改变时。
* scroll：滚动表格时。
* selectionchanged：改变选中区域时。
* sortcolumn：列被排序时。
* stylechanged：改变样式时。
* touchcancel：触摸事件被取消时。
* touchend：触摸事件结束时。
* touchmove：触摸事件发生时。
* touchstart：触摸事件开始时。

---

## classes类
### cell Abstract Class单元格抽象类
用法：
```
const grid = canvasDatagrid({
    parentNode: document.getElementById('canvasContainer'),
    schema: [...],
    data: [...]
})
grid.addEventListener('click', function (e) {
    console.log('click, e: ', e)
    console.log('click, e.active: ', e.active)
    console.log('click, e.activeHeader: ', e.activeHeader)
});
```

* active，类型boolean。为true时，该单元格为active激活状态。
* activeHeader，类型boolean。为true时，该单元格有个激活状态的表头，即该单元格和激活状态的单元格在同一行或列。
* columnIndex，类型number。该单元格的列下标。
* data，类型object。该单元格所属行的数据对象。
* formattedValue，类型string。格式化方法返回的值。详见canvasDatagrid.formatters。
* gridId，类型string。若该单元格包含了一个表格，则该值为此表格的唯一id。
* header，类型header。该单元格所属的列表头对象。
* height，类型number。canvas中该单元格的高度。
* horizontalAlignment，类型string。该单元格水平方向对齐方式。
* hovered，类型boolean。为true时，该单元格被鼠标hover。
* innerHTML，类型string。该单元格内的HTML。若有值，HTML会被渲染在该单元格内。
* isColumnHeader，类型boolean。为true时，该单元格为列表头。
* isColumnHeaderCellCap，类型boolean。为true时，该单元格为表头最右侧无内容的单元格。
* isCorner，类型boolean。为true时，该单元格为最左上角的单元格。
* isGrid，类型boolean。为true时，该单元格是一个表格。
* isHeader，类型boolean。为true时，该单元格为列或行表头。
* isRowHeader，类型boolean。为true时，该单元格为行表头。
* nodeType，类型string。固定值'canvas-datagrid-cell'。
* offsetLeft，类型number。将表格canvas当做坐标轴时，该单元格在x轴上的位置。（即该单元格左边框距离表格canvas最左边的距离。）
* offsetTop，类型number。将表格canvas当做坐标轴时，该单元格在y轴上的位置。（即该单元格上边框距离表格canvas顶部的距离。）
* parentGrid，类型canvasDatagrid。该单元格所属的表格。
* rowIndex，类型number。该单元格所在行的下标。
* rowOpen，类型boolean。为true时，该行为树形结构单元格且是展开状态。
* scrollLeft，类型number。滚动距离左侧距离。
* scrollTop，类型number。滚动距离顶部距离。
* selected，类型boolean。为true时，该单元格被选中。
* sortColumnIndex，类型number。用户重新排序后的该单元格列下标。
* sortRowIndex，类型number。用户重新排序后的该单元格行下标。
* style，类型string。该单元格的视觉样式。可以是cell单元格, activeCell激活状态的单元格, columnHeaderCell列表头单元格, cornerCell角落单元格, 或rowHeaderCell行表头单元格中任意一个。作为样式名称的前缀。
* text，类型object。该单元格的文本对象。
* text.value，类型object。类型应该为string。文本值，包含截断和省略符。
* text.width，类型object。类型应该为number。文本值的宽度，包含截断和省略符。
* text.x，类型object。类型应该为number。文本在坐标轴上x的值。
* text.y，类型object。类型应该为number。文本在坐标轴上y的值。
* type，类型string。该单元格的数据类型，由列表头定义。
* userHeight，类型number。该单元格在canvas上的高度。若为undefined，则用户没有设置该行高度。
* userWidth，类型number。该单元格在canvas上的宽度。若为undefined，则用户没有设置该列宽度。
* value，类型string。该单元格的值。
* verticalAlignment，类型string。该单元格垂直方向对齐方式。
* width，类型number。该单元格在canvas的宽度。
* x，类型number。该单元格在表格上x轴的位置。
* y，类型number。该单元格在表格上y轴的位置。

---

### contextMenuItem Abstract Class 右键菜单选项 抽象类
右键菜单中的一个选项。
可以增加、删除或者隐藏选项。下面的例子中，增加了一个右键菜单选项：
```
grid.addEventListener('contextmenu', function (e) {
    e.items.push({
        title: 'Process selected row(s)',
        click: function () {
            // e.cell.value contains the cell's value
            // e.cell.data contains the row values
            myProcess(e.cell.value, e.cell.data);
        }
    });
});
```
属性title可以用一个HTML节点来代替string。属性click非必填。详见contextmenu。

* click，类型object，选填，当选项被点击时触发的函数方法。若不执行e.stopPropagation()，会导致鼠标事件冒泡到canvas上。
* title，类型object。右键选项的名称。若是string，则直接显示string。若是HTMLElement，则会通过appendChild()方法被添加到右键菜单中，同时保有所有事件和指向。

---

### header Class 头部类
描述列数据的头。术语"头部"和"列"在此文档中会互换使用。 canvasDatagrid.schema是canvasDatagrid.header的集合数组。
* defaultValue，类型function，string。该列新行的默认值。可以是函数或者字符串。若是字符串，新单元格会直接显示该字符串。若是函数，该函数必须返回一个字符串。函数参数如下：argument[0] = canvasDatagrid.header, argument[1] = row index。
* filter，类型function。过滤该列数据的canvasDatagrid.filter函数。
* formatter，类型function。格式化该列数据的canvasDatagrid.formatter函数。
* hidden，类型boolean。为true时，该列被隐藏。这意味着，选择、复制和绘制方法都不会显示该列或该列的值。
* name，类型string。头的名字。该值必须匹配canvasDatagrid.data数组的对象属性name值。这是canvasDatagrid.header唯一一个必填的属性。除非canvasDatagrid.header.title有值，否则该name值会显示在列顶部。
* sorter，类型function。排序该列数据的canvasDatagrid.sorter函数。
* title，类型string。显示在列顶部的值。若没有该值，则会使用canvasDatagrid.header.name代替。
* type，类型string。头的数据类型。该值应匹配canvasDatagrid.formatters、canvasDatagrid.filters、canvasDatagrid.sorters的属性，在头部未定义这些值时充分利用formatting, sorting and filtering。
* width，类型number。动态列宽px值。若canvasDatagrid.attributes.allowColumnResizing被设为true，用户可以重写该值。

---

### rect Class 矩形类
选中的矩形。
* bottom，类型number。最后一行行下标。
* left，类型number。第一列列下标。
* right，类型number。最后一列列下标。
* top，类型number。第一行行下标。

---

### style Class 样式类
canvas表格样式。标准CSS样式仍然适用，但这里没有列出。

设置样式
该样式对象对所有canvas的可见元素都起效。通过该样式对象，你可以改变表格任意元素的尺寸及外形。有两类样式，一类是写入DOM元素的，比如width和margin，另一类是和canvas绘制有关的，都在style部分列出来了。

样式可以在实例化时设置。
```
var grid = canvasDatagrid({
    style: {
        gridBackgroundColor: 'red'
    }
});
```

样式可以在实例化之后设置。
```
grid.style.gridBackgroundColor = 'red';
```

使用web component方式时，样式可以按照以上方法设置，也可以使用标准CSS。
使用标准CSS时，样式名字用连字符连接，小写，并且带有'--cdg-'前缀。
```
<canvas-datagrid style="--cdg-grid-background-color: red;">[{"my": "data"}]</canvas-datagrid>
```

使用web component方式时，同样可以使用CSS classes和selectors，就像原生HTML元素一样。
```
<style>
    .my-grid {
        --cdg-grid-background-color: red;
    }
</style>

<canvas-datagrid class="my-grid">[{"my": "data"}]</canvas-datagrid>
```

你可以使用[Style Builder](https://tonygermaneri.github.io/canvas-datagrid/tutorials/styleBuilder.html)来建立个性化样式主题。

* activeCellBackgroundColor，类型string，默认值rgba(255, 255, 255, 1)。激活状态单元格的背景颜色。
* activeCellBorderColor，类型string，默认值rgba(110, 168, 255, 1)。激活状态单元格的边框颜色。
* activeCellBorderWidth，类型number，默认值1。激活状态单元格的边框宽度。
* activeCellColor，类型string，默认值rgba(0, 0, 0, 1)。激活状态单元格的字体颜色。
* activeCellFont，类型string，默认值'16px sans-serif'。激活状态单元格的字体。
* activeCellHorizontalAlignment，类型string，默认值left。激活状态单元格水平对齐方式。
* activeCellHoverBackgroundColor，类型string，默认值rgba(255, 255, 255, 1)。激活状态单元格鼠标悬浮hover时的背景颜色。
* activeCellHoverColor，类型string，默认值rgba(0, 0, 0, 1)。激活状态单元格鼠标悬浮hover时的字体颜色。
* activeCellOverlayBorderColor，类型string，默认值rgba(66, 133, 244, 1)。激活状态单元格重叠的边框颜色。
* activeCellOverlayBorderWidth，类型number，默认值1。激活状态单元格重叠的边框宽度。
* activeCellPaddingBottom，类型number，默认值5。激活状态单元格的下内边距padding bottom。
* activeCellPaddingLeft，类型number，默认值5。激活状态单元格的左内边距padding left。
* activeCellPaddingRight，类型number，默认值5。激活状态单元格的右内边距padding right。
* activeCellPaddingTop，类型number，默认值5。激活状态单元格的上内边距padding top。
* activeCellSelectedBackgroundColor，类型string，默认值rgba(236, 243, 255, 1)。激活状态单元格被选中时的背景颜色。
* activeCellSelectedColor，类型string，默认值rgba(0, 0, 0, 1)。激活状态单元格被选中时的字体颜色。
* activeCellVerticalAlignment，类型string，默认值center。激活状态单元格垂直对齐方式。
* activeHeaderCellBackgroundColor，类型string，默认值rgba(0, 0, 0, 1)。激活状态单元格对应的表头背景颜色。激活状态的表头背景颜色。无效？？？
* activeHeaderCellColor，类型string，默认值。激活状态的表头字体颜色。无效？？？
* activeRowHeaderCellBackgroundColor，类型string，默认值rgba(225, 225, 225, 1)。激活状态单元格所在行的表头单元格背景颜色。
* activeRowHeaderCellColor，类型string，默认值rgba(0, 0, 0, 1)。激活状态单元格所在行的表头单元格字体颜色。
* autocompleteBottomMargin，类型number，默认值60。右键菜单中下拉选择框距离底部的外边距。
* autosizeHeaderCellPadding，类型number，默认值8。自动调节大小的表头单元格内边距padding。？？？
* autosizePadding，类型number，默认值5。自动调节大小的内边距padding。？？？
* cellAutoResizePadding，类型number，默认值13。单元格自动调节大小的内边距padding。？？？
* cellBackgroundColor，类型string，默认值rgba(255, 255, 255, 1)。单元格背景颜色。
* cellBorderColor，类型string，默认值rgba(195, 199, 202, 1)。单元格边框颜色。
* cellBorderWidth，类型number，默认值1。单元格边框宽度。
* cellColor，类型string，默认值rgba(0, 0, 0, 1)。单元格字体颜色。
* cellFont，类型string，默认值'16px sans-serif'。单元格字体。
* cellGridHeight，类型number，默认值250。单元格表格高度。
* cellHeight，类型number，默认值24。单元格高度。
* cellHeightWithChildGrid，类型number，默认值150。包含子表格的单元格的高度。
* cellHorizontalAlignment，类型string，默认值left。单元格水平对齐方式。
* cellHoverBackgroundColor，类型string，默认值rgba(255, 255, 255, 1)。单元格鼠标悬浮时的背景颜色。
* cellHoverColor，类型string，默认值rgba(0, 0, 0, 1)。单元格鼠标悬浮时的字体颜色。
* cellLineHeight，类型number，默认值1。The line height of each wrapping line as a percentage.单元格行高，百分比。
* cellLineSpacing，类型number，默认值3。单元格行间距。
* cellPaddingBottom，类型number，默认值5。单元格的下内边距padding bottom。
* cellPaddingLeft，类型number，默认值5。单元格的左内边距padding left。
* cellPaddingRight，类型number，默认值5。单元格的右内边距padding right。
* cellPaddingTop，类型number，默认值5。单元格的上内边距padding top。
* cellSelectedBackgroundColor，类型string，默认值rgba(236, 243, 255, 1)。被选中单元格的背景颜色。
* cellSelectedColor，类型string，默认值rgba(0, 0, 0, 1)。被选中单元格的字体颜色。
* cellVerticalAlignment，类型string，默认值center。单元格垂直对齐方式。
* cellWhiteSpace，类型string，默认值nowrap。单元格内空白处理方式。可设为'nowrap'或'normal'。（normal：默认。空白会被浏览器忽略。nowrap：文本不会换行，文本会在在同一行上继续，直到遇到`<br>`标签为止。）
* cellWidth，类型number，默认值250。单元格宽度。
* cellWidthWithChildGrid，类型number，默认值250。含有表格的单元格宽度。
* childContextMenuArrowColor，类型string，默认值rgba(43, 48, 43, 1)。右键菜单中带有子菜单项的箭头颜色。
* childContextMenuArrowHTML，类型string，默认值'&#x25BA;'。右键菜单中带有子菜单项的右侧html。
* childContextMenuMarginLeft，类型number，默认值-11。右键菜单，弹出的子菜单列表框左边框距离右键菜单框右边框的距离。
* childContextMenuMarginTop，类型number，默认值-6。右键菜单，弹出的子菜单列表框上边框距离右键菜单框该父菜单上边框的距离。
* columnHeaderCellBorderColor，类型string，默认值rgba(172, 172, 172, 1)。列表头单元格边框颜色。
* columnHeaderCellBorderWidth，类型number，默认值1。列表头单元格边框宽度。
* columnHeaderCellCapBackgroundColor，类型string，默认值rgba(240, 240, 240, 1)。列表头最右侧没有内容的单元格的背景颜色。
* columnHeaderCellCapBorderColor，类型string，默认值rgba(172, 172, 172, 1)。列表头最右侧没有内容的单元格的边框颜色。
* columnHeaderCellCapBorderWidth，类型number，默认值1。列表头最右侧没有内容的单元格的边框宽度。
* columnHeaderCellColor，类型string，默认值rgba(50, 50, 50, 1)。列表头单元格字体颜色。
* columnHeaderCellFont，类型string，默认值'16px sans-serif'。列表头单元格字体。
* columnHeaderCellHeight，类型number，默认值25。列表头单元格高度。
* columnHeaderCellHorizontalAlignment，类型string，默认值left。列表头单元格水平对齐方式。
* columnHeaderCellHoverBackgroundColor，类型string，默认值rgba(235, 235, 235, 1)。列表头单元格鼠标悬浮时的背景颜色。
* columnHeaderCellHoverColor，类型string，默认值rgba(0, 0, 0, 1)。列表头单元格鼠标悬浮时的字体颜色。
* columnHeaderCellPaddingBottom，类型number，默认值5。列表头单元格下内边距。
* columnHeaderCellPaddingLeft，类型number，默认值5。列表头单元格左内边距。
* columnHeaderCellPaddingRight，类型number，默认值5。列表头单元格右内边距。
* columnHeaderCellPaddingTop，类型number，默认值5。列表头单元格上内边距。
* columnHeaderCellVerticalAlignment，类型string，默认值center。列表头单元格垂直对齐方式。
* columnHeaderOrderByArrowBorderColor，类型string，默认值rgba(195, 199, 202, 1)。列表头排序箭头的边框颜色。
* columnHeaderOrderByArrowBorderWidth，类型number，默认值1。列表头排序箭头的边框宽度。
* columnHeaderOrderByArrowColor，类型string，默认值rgba(155, 155, 155, 1)。列表头排序箭头颜色。
* columnHeaderOrderByArrowHeight，类型number，默认值8。列表头排序箭头的高度。
* columnHeaderOrderByArrowMarginLeft，类型number，默认值0。列表头排序箭头的左外边距。
* columnHeaderOrderByArrowMarginRight，类型number，默认值5。列表头排序箭头的右外边距。
* columnHeaderOrderByArrowMarginTop，类型number，默认值6。列表头排序箭头的上外边距。
* columnHeaderOrderByArrowWidth，类型number，默认值13。列表头排序箭头的宽度。
* contextFilterButtonBorder，类型string，默认值'solid 1px rgba(158, 163, 169, 1)'。右键菜单过滤按钮边框样式。
* contextFilterButtonBorderRadius，类型string，默认值'3px'。右键菜单过滤按钮边框圆角radius。
* contextFilterButtonHTML，类型string，默认值'&#x25BC;'。右键菜单过滤项中下拉菜单的下拉按钮html。
* contextFilterInputBackground，类型string，默认值rgba(255,255,255,1)。右键菜单过滤输入框背景颜色。文档未写。
* contextFilterInputBorder，类型string，默认值'solid 1px rgba(158, 163, 169, 1)'。右键菜单过滤输入框边框样式。文档未写。
* contextFilterInputBorderRadius，类型number，默认值0。右键菜单过滤输入框边框圆角。文档未写。
* contextFilterInputColor，类型string，默认值rgba(0,0,0,1)。右键菜单过滤输入框字体颜色。文档未写。
* contextFilterInputFontFamily，类型string，默认值sans-serif。右键菜单过滤输入框字体。文档未写。
* contextFilterInputFontSize，类型string，默认值14px。右键菜单过滤输入框字体大小。文档未写。
* contextFilterInvalidRegExpBackground，类型string，默认值rgba(180, 6, 1, 1)。右键菜单过滤输入框输入的正则不合法时的背景颜色。文档未写。
* contextFilterInvalidRegExpColor，类型string，默认值rgba(255, 255, 255, 1)。右键菜单过滤输入框输入的正则不合法时的字体颜色。文档未写。
* contextMenuArrowColor，类型string，默认值rgba(43, 48, 43, 1)。右键菜单用于滚动的上下箭头颜色。
* contextMenuArrowDownHTML，类型string，默认值'&#x25BC;'。右键菜单向下滚动箭头的html。
* contextMenuArrowUpHTML，类型string，默认值'&#x25B2;'。右键菜单向上滚动箭头的html。
* contextMenuBackground，类型string，默认值rgba(240, 240, 240, 1)。右键菜单背景颜色。
* contextMenuBorder，类型string，默认值'solid 1px rgba(158, 163, 169, 1)'。右键菜单边框样式。
* contextMenuBorderRadius，类型string，默认值'3px'。右键菜单边框圆角。
* contextMenuChildArrowFontSize，类型string，默认值'12px'。右键菜单子菜单箭头字体大小。
* contextMenuColor，类型string，默认值rgba(43, 48, 43, 1)。右键菜单字体颜色。
* contextMenuCursor，类型string，默认值default。右键菜单鼠标样式。
* contextMenuFilterButtonFontFamily，类型string，默认值'sans-serif'。右键菜单过滤按钮字体。文档未写。
* contextMenuFilterButtonFontSize，类型string，默认值'10px'。右键菜单过滤按钮字体大小。文档未写。
* contextMenuFilterInvalidExpresion，类型string，默认值rgba(237, 155, 156, 1)。右键菜单过滤正则验证不通过的表达式。？？？
* contextMenuFontFamily，类型string，默认值'sans-serif'。右键菜单字体。
* contextMenuFontSize，类型string，默认值'16px'。右键菜单字体大小。
* contextMenuHoverBackground，类型string，默认值rgba(182, 205, 250, 1)。右键菜单鼠标悬停时的背景颜色。
* contextMenuHoverColor，类型string，默认值rgba(43, 48, 153, 1)。右键菜单鼠标悬停时的字体颜色。
* contextMenuItemBorderRadius，类型string，默认值'3px'。右键菜单选项的边框圆角。
* contextMenuItemMargin，类型string，默认值'2px'。右键菜单选项的外边框。
* contextMenuLabelDisplay，类型string，默认值'inline-block'。右键菜单标签显示框类型。
* contextMenuLabelMargin，类型string，默认值'0 3px 0 0'。右键菜单标签的外边距。
* contextMenuLabelMaxWidth，类型string，默认值'700px'。右键菜单标签的最大宽度。
* contextMenuLabelMinWidth，类型string，默认值'75px'。右键菜单标签的最小宽度。
* contextMenuMarginLeft，类型number，默认值3。右键菜单的左外边距，即右键菜单左边框和鼠标的距离。
* contextMenuMarginTop，类型number，默认值-3。右键菜单的上外边距，即右键菜单上边框和鼠标的距离。
* contextMenuOpacity，类型string，默认值'0.98'。右键菜单的透明度。
* contextMenuPadding，类型string，默认值'2px'。右键菜单的内边距。
* contextMenuWindowMargin，类型number，默认值30。右键菜单窗口外边距。
* contextMenuZIndex，类型number，默认值10000。右键菜单的z-index值。
* cornerCellBackgroundColor，类型string，默认值rgba(240, 240, 240, 1)。左上角单元格背景颜色。
* cornerCellBorderColor，类型string，默认值rgba(202, 202, 202, 1)。左上角单元格边框颜色。、
* debugBackgroundColor，类型string，默认值rgba(0, 0, 0, .0)。debug时的背景颜色。
* debugColor，类型string，默认值rgba(255, 15, 24, 1)。debug时的字体颜色。
* debugEntitiesColor，类型string，默认值rgba(76, 231, 239, 1.00)。debug时的字符颜色。？？？
* debugFont，类型string，默认值'11px sans-serif'。debug时的字体。
* debugPerfChartBackground，类型string，默认值rgba(29, 25, 26, 1.00)。debug时性能表的背景颜色。
* debugPerfChartTextColor，类型string，默认值rgba(255, 255, 255, 0.8)。debug时性能表的字体颜色。
* debugPerformanceColor，类型string，默认值rgba(252, 255, 37, 1.00)。debug时性能颜色。
* debugScrollHeightColor，类型string，默认值rgba(248, 33, 103, 1.00)。debug时滚动高度颜色。
* debugScrollWidthColor，类型string，默认值rgba(66, 255, 27, 1.00)。debug时滚动宽度颜色。
* debugTouchPPSXColor，类型string，默认值rgba(246, 102, 24, 1.00)。debug时触摸x轴颜色。
* debugTouchPPSYColor，类型string，默认值rgba(186, 0, 255, 1.00)。debug时触摸y轴颜色。
* display，类型string，默认值'inline-block'。显示框类型。文档未写。
* editCellBackgroundColor，类型string，默认值white。编辑状态单元格背景颜色。
* editCellBorder，类型string，默认值'solid 1px rgba(110, 168, 255, 1)'。编辑状态单元格边框样式。
* editCellBoxShadow，类型string，默认值'0 2px 5px rgba(0,0,0,0.4)'。编辑状态单元格边框阴影。
* editCellColor，类型string，默认值black。编辑状态单元格字体颜色。
* editCellFontFamily，类型string，默认值sans-serif。编辑状态单元格字体。
* editCellFontSize，类型string，默认值'16px'。编辑状态单元格字体大小。
* editCellPaddingLeft，类型number，默认值4。编辑状态单元格左内边距。
* editCellZIndex，类型number，默认值10000。编辑状态单元格的z-index值。
* frozenMarkerHoverColor，类型string，默认值rgba(236, 243, 255, 1)。冻结分割线鼠标悬停时的颜色。文档未写。
* frozenMarkerHoverBorderColor，类型string，默认值rgba(110, 168, 255, 1)。冻结分割线鼠标悬停时的边框颜色。文档未写。
* frozenMarkerActiveBorderColor，类型string，默认值rgba(110, 168, 255, 1)。冻结分割线激活时的边框颜色，即鼠标拖动时的边框颜色。
* frozenMarkerActiveColor，类型string，默认值rgba(236, 243, 255, 1)。冻结分割线激活时的颜色，即鼠标拖动时的颜色。
* frozenMarkerBorderColor，类型string，默认值rgba(222, 222, 222, 1)。冻结分割线边框颜色。
* frozenMarkerBorderWidth，类型number，默认值1。冻结分割线边框宽度。
* frozenMarkerColor，类型string，默认值rgba(222, 222, 222, 1)。冻结分割线颜色。
* frozenMarkerWidth，类型number，默认值2。冻结分割线宽度。
* gridBackgroundColor，类型string，默认值rgba(240, 240, 240, 1)。表格背景颜色。
* gridBorderCollapse，类型string，默认值collapse。表格边框折叠。设为默认值collapse时，单元格的下边框会和该单元格下方的单元格上边框合为一条。另一个值expand则会显示两条边框。
* gridBorderColor，类型string，默认值rgba(202, 202, 202, 1)。表格边框颜色。
* gridBorderWidth，类型number，默认值1。表格边框宽度。
* height，类型string，默认值auto。高度。文档未写。
* maxHeight，类型number，默认值inherit。最大高度。文档未写。
* maxWidth，类型number，默认值inherit。最大宽度。文档未写。
* minColumnWidth，类型number，默认值45。最小列宽。
* minHeight，类型number，默认值inherit。最小高度。
* minRowHeight，类型number，默认值24。最小行高。
* minWidth，类型number，默认值inherit。最小宽度。文档未写。
* mobileContextMenuMargin，类型number，默认值10。移动端的右键菜单外边距。文档未写。
* mobileEditInputHeight，类型number，默认值30。移动端的编辑输入框高度。文档未写。
* mobileEditFontFamily，类型string，默认值'sans-serif'。移动端的编辑输入框字体。文档未写。
* mobileEditFontSize，类型string，默认值'16px'。移动端的编辑输入框字体大小。文档未写。
* moveOverlayBorderColor，类型string，默认值rgba(66, 133, 244, 1)。移动选中区域时的边框颜色。
* moveOverlayBorderSegments，类型string，默认值'12, 7'。移动选中区域时的边框虚线样式。
* moveOverlayBorderWidth，类型number，默认值1。移动选中区域时的边框宽度。
* name，类型string，默认值default。name样式。
* overflowX，类型string，默认值auto。设为hidden时，水平滚动条会隐藏。设为auto时，水平滚动条会在数据溢出宽度时显示。设为scroll时，水平滚动条会一直显示。
* overflowY，类型string，默认值auto。设为hidden时，垂直滚动条会隐藏。设为auto时，垂直滚动条会在数据溢出高度时显示。设为scroll时，垂直滚动条会一直显示。
* reorderMarkerBackgroundColor，类型string，默认值rgba(0, 0, 0, 0.1)。重新排序标志的背景颜色。
* reorderMarkerBorderColor，类型string，默认值rgba(0, 0, 0, 0.2)。重新排序标志的边框颜色。
* reorderMarkerBorderWidth，类型number，默认值1.25。重新排序标志的边框宽度。
* reorderMarkerIndexBorderColor，类型string，默认值rgba(66, 133, 244, 1)。重新排序标志下标边框颜色。
* reorderMarkerIndexBorderWidth，类型number，默认值2.75。重新排序标志下标边框宽度。
* rowHeaderCellBackgroundColor，类型string，默认值rgba(240, 240, 240, 1)。行表头单元格背景颜色。
* rowHeaderCellBorderColor，类型string，默认值rgba(200, 200, 200, 1)。行表头单元格边框颜色。
* rowHeaderCellBorderWidth，类型number，默认值1。行表头单元格边框宽度。
* rowHeaderCellColor，类型string，默认值rgba(50, 50, 50, 1)。行表头单元格字体颜色。
* rowHeaderCellFont，类型string，默认值'16px sans-serif'。行表头单元格字体。
* rowHeaderCellHeight，类型number，默认值25。行表头单元格高度。
* rowHeaderCellHorizontalAlignment，类型string，默认值left。行表头单元格水平对齐方式。
* rowHeaderCellHoverBackgroundColor，类型string，默认值rgba(235, 235, 235, 1)。行表头单元格鼠标悬停时的背景颜色。
* rowHeaderCellHoverColor，类型string，默认值rgba(0, 0, 0, 1)。行表头单元格鼠标悬停时的字体颜色。
* rowHeaderCellPaddingBottom，类型number，默认值5。行表头单元格下内边距。
* rowHeaderCellPaddingLeft，类型number，默认值5。行表头单元格左内边距。
* rowHeaderCellPaddingRight，类型number，默认值5。行表头单元格右内边距。
* rowHeaderCellPaddingTop，类型number，默认值5。行表头单元格上内边距。
* rowHeaderCellSelectedBackgroundColor，类型string，默认值rgba(217, 217, 217, 1)。行表头单元格被选中时的背景颜色。
* rowHeaderCellSelectedColor，类型string，默认值rgba(50, 50, 50, 1)。行表头单元格被选中时的字体颜色。
* rowHeaderCellVerticalAlignment，类型string，默认值center。行表头单元格垂直对齐方式。
* rowHeaderCellWidth，类型number，默认值57。行表头单元格宽度。
* scrollBarActiveColor，类型string，默认值rgba(125, 125, 125, 1)。滚动条被激活时的颜色。
* scrollBarBackgroundColor，类型string，默认值rgba(240, 240, 240, 1)。滚动条容器背景颜色。
* scrollBarBorderColor，类型string，默认值rgba(202, 202, 202, 1)。滚动条容器边框颜色。
* scrollBarBorderWidth，类型number，默认值0.5。滚动条容器边框宽度。
* scrollBarBoxBorderRadius，类型number，默认值4.125。滚动条边框圆角。
* scrollBarBoxColor，类型string，默认值rgba(192, 192, 192, 1)。滚动条颜色。
* scrollBarBoxMargin，类型number，默认值2。滚动条外边距。
* scrollBarBoxMinSize，类型number，默认值15。滚动条最小尺寸。
* scrollBarBoxWidth，类型number，默认值8。滚动条宽度。
* scrollBarCornerBackgroundColor，类型string，默认值rgba(240, 240, 240, 1)。滚动条最下角落背景颜色。
* scrollBarCornerBorderColor，类型string，默认值rgba(202, 202, 202, 1)。滚动条最下角落边框颜色。
* scrollBarWidth，类型number，默认值11。滚动条容器宽度。
* selectionHandleBorderColor，类型string，默认值rgba(255, 255, 255, 1)。选中区域操作手势的边框颜色。
* selectionHandleBorderWidth，类型number，默认值1.5。选中区域操作手势的边框宽度。
* selectionHandleColor，类型string，默认值rgba(66, 133, 244, 1)。选中区域操作手势的颜色。
* selectionHandleSize，类型number，默认值8。选中区域操作手势的尺寸。
* selectionHandleType，类型string，默认值square。选中区域操作手势的类型。可设为square或circle。
* selectionOverlayBorderColor，类型string，默认值rgba(66, 133, 244, 1)。选中区域边框颜色。
* selectionOverlayBorderWidth，类型number，默认值1。选中区域边框宽度。
* treeArrowBorderColor，类型string，默认值rgba(195, 199, 202, 1)。树形结构箭头边框颜色。
* treeArrowBorderWidth，类型number，默认值1。树形结构箭头边框宽度。
* treeArrowClickRadius，类型number，默认值5。树形结构点击的边框圆角。？？？
* treeArrowColor，类型string，默认值rgba(155, 155, 155, 1)。树形结构箭头颜色。
* treeArrowHeight，类型number，默认值8。树形结构箭头高度。
* treeArrowMarginLeft，类型number，默认值0。树形结构箭头左外边距。
* treeArrowMarginRight，类型number，默认值5。树形结构箭头右外边距。
* treeArrowMarginTop，类型number，默认值6。树形结构箭头上外边距。
* treeArrowWidth，类型number，默认值13。树形结构箭头宽度。
* treeGridHeight，类型number，默认值6。树形结构表格高度。
* width，类型number，默认值auto。宽度。文档未写。

---
