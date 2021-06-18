## 事件

事件分类: 

+ 网络编程中的事件，node中的监听事件
+ 网页中的事件（重点学习）

使用网页事件的三种方式

+ 行内事件处理器（不建议使用，已经过时）
+ 事件处理器属性（尽量不适用）
+ addEventListener()和removeEventListener()推荐使用

```js
function changeColor() {
  console.log('颜色改变了')
}

const btn = doucument.querySelector('#btn')
btn.addEventListener('click', changeColor) // 添加事件处理程序  第三个参数设置为true 事件为事件捕获
btn.removeEventListener('click', changeColor) // 移除事件处理程序

```

> 注意： addEventListener可以为同一个dom对象添加多个事件处理程序，事件处理器属性只能添加一个，重复定义会被覆盖

### 事件对象

事件处理程序的参数e或者event或者evt等，指的是事件对象

重点使用的几个属性

e.target > 始终指向事件刚刚发生的元素的引用

e.preventDetault() > 阻止默认行为

```html
<body>
  <div>
    <form action="www.baidu.com" method="get">
      <label for="name">
        用户名: 
        <input type="text" id="name">
      </label>
      <label for="age">
        年龄: 
        <input type="text" id="age">
      </label>
      <button type="submit" id="btn">提交</button>
    </form>
  </div>
</body>
<script>
  const btn = document.querySelector('#btn')
  btn.addEventListener('click',  e => {
    e.preventDefault()
    console.log('点击了，触发事件1')
  })
</script>
```

e.stopPropagation() > 阻止事件冒泡

### 事件冒泡和事件捕获

+ 事件捕获：
  + 浏览器检查元素的最外层`<html>`，是否在捕获阶段中注册一个`onclick`事件，如果是，则运行这个事件
  + 否则，检查`<html>`的直接子元素，执行上面的操作，一次类推，直到到达实际点击的元素
+ 事件冒泡：
  + 浏览器检查实际点击的元素是否在冒泡阶段中注册了一个`onclick`事件处理程序，如果是，则运行它
  + 否则向该元素的父元素，并做同样的事，直到到达`<html>`元素

### 事件委托

利用事件冒泡，我们可以使用事件委托，如果你想在大量子元素中点击任意一个，都可以运行一段代码，可以将事件监听器设置在父元素上，并让子节点上发生的事件冒泡到父节点上，从而不用为每一个子元素设置一个事件处理程序





### 总结

事件并不是js的核心部分，他们是浏览器webAPI中定义的





