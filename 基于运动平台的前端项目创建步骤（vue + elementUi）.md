# 基于运动平台的前端项目创建步骤（vue + elementUi）

## 1.创建前端项目：

1.1在已经创建好的vue项目下执行vue ui命令（vue ui为图形化界面）

![image-20220527101733584](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527101733584.png)

创建成功后会跳转到对应的页面

![image-20220527101852395](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527101852395.png)

如果之前已经有创建过vue项目，则点击左下角跳转到项目管理器

![image-20220527102910578](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527102910578.png)



创建脚手架后 点击这其中的几个标签，会为你选择文件路径

![image-20220527103608623](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527103608623.png)

![image-20220527103515653](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527103515653.png)



![image-20220527103806589](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527103806589.png)



![image-20220527103825292](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527103825292.png)



在选择css预处理器时选择dart-scss



选择继续而不保存：

![image-20220527105117749](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527105117749.png)

## 2.安装插件跟依赖

安装element ui 插件 vue2的话暗转element ui

anxios依赖

less依赖

lessloader依赖

把app.vue里面的组件清空

![image-20220527111413180](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527111413180.png)

删除view的组件

把修改index.js里面的内容

![image-20220527111855286](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527111855286.png)

## 3.login组件创建(相当于html)



3.1创建login组件

3.2在路由中引入组件路径

3.3配置路径 

![image-20220527222251567](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527222251567.png)

3.4 在app里面加入

<router-view></router-view>

在这里就可以测试login里面组件有没有成功引入，运行vue项目



3.5 对login布局进行分析

3.6 添加全局样式

![image-20220527223640164](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527223640164.png)

在main.js里面引入全局样式，因为main.js就是用来放全局的 



3.7 创建表单区域() 在element ui里面引入

想要引入就能用，就先不要绑定数据(把v-model删掉) 如果要绑定数据的话 要在data里面设置配置项

![image-20220527231142293](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527231142293.png)

绑定的数据

![image-20220527231506820](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527231506820.png

表单的配置

![image-20220527231834217](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527231834217.png)

这里把表单看作一个对象，里面的输入框跟按钮相当于属性 

注意表单和按钮等的v-model，这里跟data数据绑定，以及访问的方式有关



3.8 css中引入lang="less"的时候，会出现less版本不兼容的情况 这时需要：

卸载less版本 ：npm uninstall less-loader

安装版本：npm install less-loader@5.0.0 --save（这是网上很多推荐的版本）

要根据自己的情况而定 比如我电脑需要安装的版本为：![image-20220528125229590](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220528125229590.png)

安装完成后记得重启vsode 

vscode的重启方式为：![image-20220528125349115](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220528125349115.png)

如果权限出现问题输入的命令错误，可以通过管理员方式打开

这里的命令方式指的是：npm install less-loader@5.0.0



3.9  iconfont的引入

在element ui中有带 icon 的输入框

通过prefix-icon等来放置图标

如果想要更多的iconfont图标可以在www.iconfont.cn 下载图标，保存到相应的项目中，引入到vscode里面

icon文件里面有一个html文件 打开这个文件 选择fontclass引用，更具要求，在main.js里卖引入相应的文件

在相应的控件中获取iconfont 的class名称

3.10样式编写



3.11 login校验规则



element ui中需要绑定:rules="rules"属性 在输入框中填写prop属性 :



![image-20220528142146102](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220528142146102.png)



![image-20220528142249242](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220528142249242.png)

填写完要记得使用v-model绑定loginFome 

## 4.home组件的创建

### 4.1 创建home组件 

组件创建完成后要在路由中的index.js路径引入home,再在router添加路径

![image-20220530145338007](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220530145338007.png)



![image-20220530145420457](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220530145420457.png)

### 4.2 页面跳转

在methods中书写login方法 登录按钮绑定@click="login"

![image-20220530150525822](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220530150525822.png)



### 4.3 布局跟header

在element ui 中使用containner（这个组件外部不用嵌套div）组件布局

书写样式（header,aside,main）

可以使用element ui自身携带的样式，也可以自己编写

但是在编写时要注意侧边栏的高度问题

![image-20220530165432845](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220530165432845.png)

加入这个后变成这样：

.home-containner {

 height: 100%;

}

![image-20220530165531744](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220530165531744.png)

### 4.4 加入菜单栏（侧边栏绘制）

根据需求而定（一级菜单栏，或者二级菜单栏）

在创建菜单栏时一定要多注意 不要把组件引入错 要多练习）

![image-20220531203856391](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531203856391.png)

我们希望在加载页面时数据就会出来

onload事件

所以用 created() {

​		查询getMenuList

​       this.getMenuList();

​    },

### 4.5 导航对象

后端接口部分

### 4.6 获取导航数据（只是在页面中展示）

在进行布局时要细心

需求：页面加载时显示数据 在加载页面数据时可以先用console.log()测试数据是否有显示

 created() {

​      *//查询menuList 什么时候发生呢，create的时候发生*

​       this.getMenuList();

   },

methods: {

​      *//获取导航菜单方法*

​      async getMenuList(){

​       *// 获取springboot controller接口的路径*

​        const{data:res} = await this.$http.get("menus");

​        console.log(res);

​        if(res.flag!=200) return this.$message.error("获取列表失败")

​         //取出的数据反填到menulist中*

​         this.menuList=res.menus; 

​      }，

 }

要把接口查询的数据传给menuList对象

先用插值语法测试    

![image-20220601001539707](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220601001539707.png)

### 4.7导航栏数据绘制（显示在固定的区域，相当于页面传值）

一级菜单中显示：

菜单栏中的值得在menulist对象里卖获取，而menulist为数组，所以通过v-for遍历得到

v-for="item in menulist"  遍历完根据需求查找数据库中与之对应的值

用插值语法在页面中显示

二级菜单显示的原理一级菜单的显示差不多，只是有一点要注意的是，遍历的对象不同

v-for="it in item.subMenuList" 

这个subMenuLis代表的是pojo类中对象里面的一个属性(一堆对象里面的一个对象)

![image-20220601002455267](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220601002455267.png)



但是这里会出现一个问题，点击一个菜单，其它菜单都会被选中，解决的方法是

index="item.id+'' '',进行动态绑定

![image-20220601003109064](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220601003109064.png)



### 4.8 main区域重定向

分析：点击用户列表，展示在main区域 

在home页面的main区域加入路由组件<router-view></router-view>

添加相关的子组件：welcome.vue

在路由的index.js文件里面添加路由路径 因为main区域的组件属于home的子组件 

所以要在home里面添加子路由：

重定向：

redirect:"/welcom"

{path:"/welcome",component:Welcome}

要统一大小写，路径，重定向等一般写小写，组件一般写大写

### 4.9 侧边导航区域路由

有一个问题：一个一级菜单下有很多个二级菜单 不可能每一个菜单都要写一个页面

方法：在el-menu 中绑定： :router="true"  

根据mainmenu表中的path路径进行定位：（可以观察博客项目中的表结构是否有用到这种方法）

但是定位到相应的页面时页面的内容怎么写

![image-20220601220748900](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220601220748900.png)

component组件里面加一个文件夹，里面放置userlist组件

index.js里面添加路由路径

:index="it.id"中id改成path 这里要了解绑定:index是什么意思
