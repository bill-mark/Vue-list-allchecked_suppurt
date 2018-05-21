# Vue-list-allchecked_suppurt
vue下拉list支持全选功能

导语:Vue中单选下拉框开发起来非常简单,直接select包裹一个带v-for的option即可

![basic](https://github.com/bill-mark/Vue-list-allchecked_suppurt/blob/master/static/1.png)


       但是当我们想做个带多选的下拉框该怎么办呢?最简方法是什么?比如下面这个图:
![basic](https://github.com/bill-mark/Vue-list-allchecked_suppurt/blob/master/static/2.png)

如果网上搜的话,搜的是一堆带children的 ,那种是遍历tree的思想,和多选下拉框不是一回事,而且写起了复杂

话不多说,先上源码,GitHub - bill-mark/Vue-list-allchecked_suppurt: vue下拉list支持全选功能看不懂源码再往下读:

需求:后端传前端一个数组对象,每个对象有id和name,前端把被选中的对象的id传给后端.

分析:前端先声明一个空数组,拿到后端返回的数组对象后,新增一个name为全部的对象,下面是源码例子

![basic](https://github.com/bill-mark/Vue-list-allchecked_suppurt/blob/master/static/3.png)


接下来写HTML:
![basic](https://github.com/bill-mark/Vue-list-allchecked_suppurt/blob/master/static/4.png)

下面就是JS了:

    JS只watch这个数组不需要写额外的方法,够简单吧. 

     核心点有两个:

            1.Vue想watch一个数组对象的变化,需要声明为deep  就是深度watch的意思.

                原因:Vue会把data遍历成一个树,只watch指定的节点本身,如果节点还有子节点不会管,加个deep是让Vue也watch子节点

            2.name为'全部'的对象,比其他对象多了一个last_state属性

               因为JS中把一个数组赋值一个变量,其实是这个变量的引用指向这个数组.在Vue的watch中,旧值与新值的引用指向同一个数组,当用户点了全选,判断不了全选之前的状态是被选中还是没被选中,所以要把上一个状态存在last_state中,当用户点了全选,如果last_state为true说明是取消全选的操作,如果last_state为false说明是勾选全选的操作
非核心点有一个:

               怎么实现子全选后,全选框被勾选呢?或者全部勾选后,去掉一个子节点,怎么把父(伪)节点也去掉呢?

               解决方案:在watch中声明空数组,然后把state为true的元素加入进来,剩下的就是比较判断了,

                最后把watch声明的空数组的id取出来传给后端即可 
                
 贴段watch代码
 ![basic](https://github.com/bill-mark/Vue-list-allchecked_suppurt/blob/master/static/5.png)
