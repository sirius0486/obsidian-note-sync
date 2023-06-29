```js
// 1. 获取 URL 参数

let params = new URLSearchParams(window.location.search);
// params.get('paramName')

// 2. 深度复制对象
let cloneObj = JSON.parse(JSON.stringify(obj));

// 3. 生成随机颜色

let randomColor = "#" + Math.floor(Math.random() * 16777215).toString(16);

// 4. 计算数组中的最大值
let max = Math.max(...array);

// 5. 生成指定范围内的随机整数
let randomInt = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
```

Window 对象是浏览器全局对象，表示浏览器应用窗口，包含许多与浏览器相关的属性和方法，例如 window.document、window.navigator、window.location 等等。通过这些属性和方法，我们可以访问和操作 HTML 页面的元素和内容，以及获取与浏览器相关的信息。

例如:
- window.document 可以直接操纵 HTML 文档，对页面上的元素进行增删改查。
- window.location 可以让我们访问当前页面的 URL，并且可以用于重定向用户到其他页面。
- window.history 可以操作浏览器的历史记录 ，如 back() 和 forward()。
- window.resizeTo() 和 window.moveTo() 可以调整浏览器窗口的大小或位置。
- window.open() 可以打开新的浏览器窗口。
- window.close() 可以关闭浏览器窗口。

需要注意的是，并非所有这些属性和方法都能正常使用，因为浏览器可能出于安全原因，会把它们禁用。