* UniApp
    - 同一套代码编译多端
    - 接近原生，效果更好
    - 开发效率高，成本降低，学习成本低
    - 支持npm与自定义组件
    - 社区活跃，版本迭代快
* 框架基础
    - MVC与MVVM思想
        MVC：后端思想
         view<--->Controller<--->Model

        --->M：model-模型层，数据的增删改查
        --->V：view-视图层，前端页面（html/js/css）
        --->C：controller-控制层，处理业务
        MVVM：
          View( 页面HTML)<--->ViewModel（核心调度者协调器在script里，数据双向绑定）<--->Model（单页面的静态数据，在script>的data里）

* 应用生命周期
    - onLaunch（当uni-app初始化完成时触发，全局只触发一次）
    - onShow（启动，或从后台进入前台显示时）
    - onHide（从前台进入后台时）
    - onUniNViewMessage
* 页面生命周期
    - onLoad 监听页面加载
    - onUnload 监听页面卸载
    - onShow 监听页面显示
    - onHide 监听页面隐藏
    - onReady 监听页面初次渲染完成
* 数据绑定
    - 在标签外部时，使用：{{表达式}} ，当在标签内部时，用v-bind：/：
    - 动态数据绑定时，比如src 要在前面加：
* 事件处理
* 条件渲染（全支持vue） 和列表循环（v-for）
    - v-if和v-show的区别：前者 ：是否会在dom中被移除，后者display：none
    - v-for里要 :key=“index” 保证组件和数据捆绑唯一。
        --->嵌套循环的时候，:key的内容要不同
* ifdef和ifndef （条件编译）
    - ifdef 只在什么地方编译
    - ifndef 除了不在什么地方编译，在其他地方都编译
    - 可以在html、js、css里写
    - 写在注释里
        --->html里   <!--#ifdef MP --> <!--#endif-->
        --->js里    //#ifdef MP-WEIXIN  //#endif
        --->style里  /* #ifdef H5 */    /* #endif */    只在H5...
