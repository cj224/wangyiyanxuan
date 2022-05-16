# wangyiyanxaun
网易严选静态页面练习

从5月11号开始写网易严选的项目练习，有了写小米商城项目的经验，所以基本上排版和布局都没有遇到问题，但也花了接近五天的时间才写完，有首页、商品详情页和商品列表页，这次练习加深了排版和布局的理解，浮动定位的运用也越来越熟练。

浅谈一下收获吧：

### 定位关系

1. ###### 没有浮动和定位的正常情况下，后写的元素会比先写的元素层级高。

   <img src="https://jjimg-1309015283.cos.ap-chengdu.myqcloud.com/image-20220516144913170.png" alt="image-20220516144913170" style="zoom:25%;" />

   ```
   .bigbox{
       width: 400px;
       height: 400px;
       background-color: orange;
       margin: 50px auto 0;
   }
   .box1{
       width: 200px;
       height: 100px;
       background-color: red;
   }
   .box2{
       width: 100px;
       height: 200px;
       background-color: blue;
       margin-top: -20px;
   }
   
   <div class="bigbox">
       <div class="box1"></div>
       <div class="box2"></div>
   </div>
   ```

   

2. ###### 当给`box1`设置左浮动时，`box1`会脱离文档流浮动起来，`box2`会顶上去。

   <img src="https://jjimg-1309015283.cos.ap-chengdu.myqcloud.com/image-20220516145259607.png" alt="image-20220516145259607" style="zoom:25%;" />

   ```css
   .box1{
       width: 200px;
       height: 100px;
       background-color: red;
       float: left;
   }
   ```

   

3. ###### 当给 `bigbox`设置相对定位，`box1`左浮动，`box2`相对定位时，`box2`的层级比 `box1`的层级高，说明定位比浮动的层级高。此时 `box2`相对 `bigbox`定位，`margin-top:-20px;`会把 `bigbox`的 `margin-top`也 `-20px`。设置top则不会。

   <img src="https://jjimg-1309015283.cos.ap-chengdu.myqcloud.com/image-20220516150448369.png" alt="image-20220516150448369" style="zoom:25%;" />

   ```css
   .bigbox{
       width: 400px;
       height: 400px;
       background-color: orange;
       margin: 50px auto 0;
       position: relative;
   }
   .box1{
       width: 200px;
       height: 100px;
       background-color: red;
       float: left;
   }
   .box2{
       width: 100px;
       height: 200px;
       background-color: blue;
       margin-top: -20px;
       position: relative;
   }
   ```

   

4. ###### 当 `box1`和 `box2`都改成绝对定位时，他们会脱离文档流，`margin-top`不影响父元素。

   <img src="https://jjimg-1309015283.cos.ap-chengdu.myqcloud.com/image-20220516150636256.png" alt="image-20220516150636256" style="zoom:25%;" />

   ```css
   .box1{
       width: 200px;
       height: 100px;
       background-color: red;
       position: absolute;
   }
   .box2{
       width: 100px;
       height: 200px;	
       background-color: blue;
       margin-top: -20px;
       position: absolute;
   }
   ```

   

5. ###### 想要改变层级可以使用 `z-index`属性（前提是只对定位元素生效），两个兄弟元素之间值越大层级越高。

   <img src="https://jjimg-1309015283.cos.ap-chengdu.myqcloud.com/image-20220516151730247.png" alt="image-20220516151730247" style="zoom:25%;" />

6. ###### 总结：标准流盒子，低于浮动的盒子，浮动的盒子又低于定位的盒子，两个设了定位的兄弟元素之间`z-index`数值越大层级越高。



### `calc()`函数

`calc()` 函数用于动态计算长度值。

- 需要注意的是，运算符前后都需要保留一个空格，例如：`width: calc(100% - 10px)`；
- 任何长度值都可以使用`calc()`函数进行计算；
- `calc()`函数支持 "+", "-", "*", "/" 运算；
- `calc()`函数使用标准的数学运算优先级规则；
