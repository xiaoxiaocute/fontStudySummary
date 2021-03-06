表格细线边框

```js
    每个单元格都可以看作是一个盒子 设置盒子边框可以使用border
    但是border盒子边框线的宽度会有叠加的效果
    因此需要合并边框线的宽度
    border-collapse:collapse;   //相邻的边框合并在一起
```

边框会影响盒子的实际大小
解决方案: 1.测量盒子的大小的时候,不测量边框 2.如果测量了边框就需要 width/height 减去边框的宽度

内边距: 盒子边框与内容之间的距离

```js
    padding: 5px  代表上下左右都有5px内边距
    padding: 5px 10px  代表上下内边距是5px  左右内边距是10px
    padding: 5px 10px 20px 代表上5px 左右10px  下20px
    padding: 5px 10px 20px 30px  代表上5px 右10px 下20px 左30px
```

padding 实际应用场景

```js
    当内容的宽度不确定的时候 给盒子固定的宽度是不合理的
    要解决这类问题 给盒子padding比较合理
```

padding 不会撑开盒子的情况

```js
    不指定盒子的688888888888888888888承父盒子的宽度 指定的padding值 不会撑开盒子
```

外边距的经典案例
块级盒子水平居中

```js
    外边距水平居中必须满足条件:
    1.盒子必须指定宽度
    2.盒子左右外边距都设置为auto
```

行内元素或者行内块元素水平居中

```js
    行内元素或者行内块元素水平居中就给其父元素添加text-align:center即可
```

外边距合并

```js
1.当相邻的两个元素相遇时,如果上面的元素有下外边距margin-bottom
下面的元素有margin-top 则他们之间的垂直间距不是margin-bottom和margin-top的和
取两个值中的较大者 这种现象称之为 相邻块元素垂直外边距的合并
2.嵌套元素外边距塌陷
对于两个嵌套关系的块元素 父元素有上外边距同时子元素也有上外边距
此时父元素会塌陷较大的外边距值
```

解决外边距塌陷

```js
方式一: 可以为父元素定义上边框;
方式二: 可以为父元素定义上内边距;
方式三: 可以为父元素添加overflow: hidden;
```

行内元素只设置左右内外边距 不设置上下内外边距

CSS3 新增
圆角边框
盒子阴影

```js
    box-shadow: h-shadow v-shadow blur spread color inset
        h-shadow: 必需 水平阴影的位置 允许负值
        v-shadow: 必需 垂直阴影的位置 允许负值
            blur: 可选 模糊距离
          spread: 可选 阴影的尺寸
           color: 可选 阴影的颜色
           inset: 可选 将外部阴影改为内部阴影
```

文字阴影

float 元素的特征:

```js
1.脱离标准流 浮动的盒子不会保留原先的位置
2. 如果多个盒子都设置了浮动 则他们会按照属性值一行内显示并顶端对齐排列
注意:
浮动的元素是相互贴靠在一起的 不会有缝隙
如果父级宽度装不下这些浮动的盒子 多出来的盒子会另起一行对齐
3.浮动的盒子会有行内块元素的特性
如果行内元素有了浮动 则不需要转换会计/行内块元素就恶意直接给宽度和高度
块级元素默认宽度和父级宽度一样 如果有了浮动 块级元素的宽度则和内容一样宽
```

为什么要清除浮动

```js
    并不是所有的父盒子都有高度的。
    需求：让子盒子撑开父盒子 不给父盒子固定的高度
    如果子盒子都加浮动了 父盒子的高度就变成0了  因为浮动的盒子不占位置  这样的话 其他的盒子会占用父盒子的高度了
```

清除浮动

```js
    清除浮动就是清除浮动造成的影响
    清除浮动的本质就是清除浮动元素脱离标准流造成的影响
    clear: both
    清除浮动的方法:
        1.额外标签法(隔墙法): 在最后一个浮动的盒子后面添加一个标签  新增的盒子必须是块级元素 不能是行内元素
        2.父级添加overflow属性
        3.父级添加after伪元素
        .clearfix:after{
            content: "";
            display: block;
            height: 0;
            clear: both;
            visibility: hidden;
        }
        .clearfix {
            *zoom: 1;
        }
        4.父级添加双伪元素
        .clearfix:before,.clearfix:after {
            content: "",
            display: table
        }
        .clearfix:after {
            clear: both
        }
        .clearfix {
            *zoom: 1;
        }
```
