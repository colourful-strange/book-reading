### 概述

#### CSS3出现的历史和背景

1. iPhone X等设备顶部的“刘海儿”和底部的触摸横条会和页面内 容冲突，所以需要env()函数给网页设置安全距离。

   ```css
   body {
       padding-top: env(safe-area-inset-top);
       padding-right: env(safe-area-inset-right);
       padding-bottom: env(safe-area-inset-bottom);
       padding-left: env(safe-area-inset-left);
   }
   
   ```

2. 围绕四个方向

   - 更复杂、更具弹性的布局的支持，如弹性布局、网格布局等; 

   - 更丰富的视觉表现的支持，如圆角、盒阴影、动画和渐变等; 
   - 更多样的浏览设备的支持，如CSS Media Queries媒体查询等; 
   - 开发者CSS自定义能力的支持，如CSS Houdini等。

#### 模块化的CSS新世界

1. 模块化优点是可以快速使用某些新特性；缺点是设计冗余，需要记住多个属性。

### 需要提前了解的知识

#### 互通互连的[**CSS数据类型**](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Types)

1. 数据类型由放置在不等式符号 "<" 和 ">" 之间的关键字表示。任何CSS属性值一定包含一个或多个数据类型。

2. ```css
   background-image:none | <image>
   ```

   <image>就是一种数据类型，包括这些类型和函数：

   - <url>
   - <gradient>
   -  element()
   -  image()
   -  image-set()
   -  cross-fade()

3. CSS数据类型除了可以帮助我们快速掌握CSS的语法，还能快速更 新整个CSS世界的知识库。

#### 几个常见数据类型简单介绍

1. [<shape-box>](https://developer.mozilla.org/zh-CN/docs/Web/CSS/shape-outside#shape-box)
2. [<base-shape>](https://developer.mozilla.org/zh-CN/docs/Web/CSS/basic-shape)
3. [<image>](https://developer.mozilla.org/zh-CN/docs/Web/CSS/image)
4. [<color>](https://developer.mozilla.org/zh-CN/docs/Web/CSS/color_value)
5. [CSS值类型文档大全](https://www.zhangxinxu.com/wordpress/2019/11/css-value-type/)

#### 学会看懂CSS属性值定义的语法

1. 有些CSS属性值是可以省略的，看懂这些值，可以帮助我们写出更简洁的代码。

2. 关键字。部分CSS属性支持的属于通用关键字（auto,none,ease）。被所有CSS属性支持的属于全局关键字（inherit,ininial,unset,revert）。

3. CSS语法中的符号分为字面符号、组合符号和数量符号。

   1.  字面符号指的是CSS属性值中原本就支持的合法符号。

      ![字面符号](https://cdn.jsdelivr.net/gh/colourful96/ImagePicGo@main/img/img/%E5%AD%97%E9%9D%A2%E7%AC%A6%E5%8F%B7.png)

   2. 组合符号用来表示数个基本元素之间的组合关系。

      ![组合符号](https://cdn.jsdelivr.net/gh/colourful96/ImagePicGo@main/img/img/%E7%BB%84%E5%90%88%E7%AC%A6%E5%8F%B7.png)

   3. 数量符号用来描述一个元素可以出现多少次，数量符号不 能叠加出现，并且优先级高于组合符号。

      ![数量符号](https://cdn.jsdelivr.net/gh/colourful96/ImagePicGo@main/img/img/%E6%95%B0%E9%87%8F%E7%AC%A6%E5%8F%B7.png)

4. 凡是出现斜杠（/）的地方，斜杠前后的数据 类型一定是相同或者部分相同的，否则整个语句就是非法的。

#### 了解CSS全局关键字属性值

##### inherit

1. 实用性和兼容性都很好的属性。可以多使用，有效减低维护和开发成本。

##### initial

1. initial是初始值关键字，可以把当前的CSS属性的计算值还原 成CSS语法中规定的初始值。
2. 需要重置某些CSS样式，但又不记得初始值。
3. initial设置的初始值和浏览器设置元素的初始值是不一样的。

##### unset

1. 一般配合all使用: all: unset。如果需要批量重置某个元素的默认样式，则使用该属性。

##### revert

1. revert关键字可以让当前元素的样式还原成浏览器内置的样式。
2. 没有任何理由对*li*元素进行任何样式重置。

#### 指代所有CSS属性的all属性

1. all属性可以重置除unicode-bidi、direction以及CSS自定 义属性以外的所有CSS属性。
2. all:unset 可以让任意一个元素样式表现和元素一样。all:revert可 以让元素恢复成浏览器默认的样式，也是很有用的。

#### CSS新特性的渐进增强处理技巧

1. 不需要在这样写

   ```css
   /* IE8+ */
   display: table-cell;
   /* IE7 */
   *display: inline-block;
   /* IE6 */
   _display: inline;
   ```

#### 直接使用CSS新特性

1. 直接使用CSS新属性即可，支持的浏览器体验更好，不支持的会保持原样。

#### 利用属性值的语法差异实现兼容

 ```css
 .icon-loading {
 display: inline-block;
 width: 30px; height: 30px;
 /* 所有浏览器识别 */
 background: url(./loading.gif);
 /* IE10+浏览器识别，覆盖上一行background声明 */
 background: url(./loading.png), linear-gradient(transparent,
 transparent);
 animation: spin 1s linear infinite;
 }
 @keyframes spin {
 from { transform: rotate(360deg); }
 to { transform: rotate(0deg); }
 }
 ```

```css
// #00000000 可以通过不支持的属性实现兼容
.background-pattern {
background: url(./pattern.png);
background: repeating-linear-gradient(...), repeating-lineargradient(...), #00000000;
background-blend-mode: multiply;
}
```

#### 借助伪类或伪元素区分浏览器的技巧

1. CSS选择器语句中如果存在浏览器无法识别的伪类或伪元素，整个CSS 规则集都会被忽略。

2. IE9+

   ```css
   /* IE9+浏览器识别 */
   _::before, .some-class {}
   /* 或者 */
   _::after, .some-class {}
   /* 或者 */
   _::selection, .some-class {}
   
   _:checked, .some-class {}
   /* 或者 */
   _:disabled, .some-class {}
   ```

3. IE10+  :required、 :optional、:valid、:invalid  animation
4. IE11+ ::backdrop  -ms-私有前缀
5. 浏览器类型的区分  -moz- -webkit- -ms-

#### @supports规则下的渐进增强处理

1. 可以用来检测当前浏览器 是否支持某个CSS新特性，这是最规范、最正统的CSS渐进增强处理方 法。

2. ```css
   /* 支持弹性布局 */
   @supports (display: flex) {}
   /* 不支持弹性布局 */
   @supports not (display: flex) {}
   /* 同时支持弹性布局和网格布局 */
   @supports (display: flex) and (display: grid) {}
   /* 支持弹性布局或者支持网格布局 */
   @supports (display: flex) or (display: grid) {}
   
   /* 合法 */
   @supports (display: flex) and (display: grid) and (gap: 0) {}
   @supports (display: flex) or (display: grid) or (gap: 0) {}
   ```

##### @supports规则完整语法和细节

1. 浏览器还提供了CSS.supports()接口，让我们可以在 JavaScript代码中检测当前浏览器是否支持某个CSS特性。

   ```javascript
   CSS.supports(propertyName, value);
   CSS.supports(supportCondition);
   ```

2. @supports规则的花括号可以包含其他任意@规则，甚至是 包含@supports规则自身。

   ```css
   @supports (display: flex) {
   /* 支持内嵌媒体查询语法 */
   @media screen and (max-width: 9999px) {
   .supports-match {
   color: #fff;
   }
   }
   /* 支持内嵌@supports语法 */
   @supports (animation: none) {
   .supports-match {
   animation: colorful 1s linear alternate infinite;
   }
   }
   /* 支持内嵌@keyframes语法 */
   @keyframes colorful {
   from { background-color: deepskyblue; }
   to { background-color: deeppink; }
   }
   }
   ```

   

### CSS属性

1. *env()* : 环境变量
2. *mask-image*: 用作元素蒙版层的图像
3. Shapes布局  *shape-outside*: 定义了一个可以是非矩形的形状
4. *unicode-bidi*： 决定如何处理文档中的双书写方向文本
5. *direction*: 设置文本、表格列和水平溢出的方向
6. [@supports](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@supports) 检测浏览器是否支持某个CSS属性

