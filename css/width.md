### width=auto
> width的默认值为auto

+ 宽度100%  div p等块元素
+ 宽度为内容的宽度   设置了绝对定位、行内块元素、浮动、table元素
+ 宽度超出父元素     white-space: nowrap;

以上的几种情况可以分类为内部尺寸决定宽度和外部尺寸决定宽度。


#### 1-1外部尺寸
> 第一种为**外部尺寸**决定元素的宽度，后边几种都是内部尺寸决定元素的宽度，这个外部尺寸就是流【flow】

#####  正常流宽度

Width: auto;

##### 格式化尺寸

元素的position属性为absolute或者fixed时，当相对的方向的值同时存在，就会出现格式化尺寸

```css
div { position: absolute; left: 20px; right: 20px; }  
/* content margin padding会自动计算分配水平方向的尺寸*/
```

#### 2 内部尺寸和流体特征

> 内部尺寸就是由元素内部决定的

```css
display: inline-block;
position: absolute;
float: left
```

包裹性：内容不会超出元素的边界

首选最小宽度：就是单个汉字或者英文单词的宽度

最大宽度为：元素内部连续内联盒子的宽度之和

#### 3 宽度分离

```css
.box {
  width: 200px;
  padding: 10px;
}
// 这样写不好 为什么  丧失了流动性  比较好的写法如下
.father {
  width: 300px;
}
.child {
  padding: 10px;
}
// 或者使用
.box {
  box-sizing: border-box; // 全线支持
  padding: 10px;
}
```





