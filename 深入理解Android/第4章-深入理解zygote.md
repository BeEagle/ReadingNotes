# 第4章-深入理解zygote



zygote 受精卵



system_server  



## zygote 分析



zygote 是**由 init进程根据 init.rc 文件中的配置项创建的**。

zygote 最初叫 app_process，通过 pctrl 系统将自己的名字换成了 zygote。



app_process 对应 `App_main.cpp`



App_main的 main 方法里调用了 `AppRuntime.start` (AppRuntime.cpp)。



该方法非常的关键，主要做了如下几件事，可以说是为Java 世界准备好了一切。



1. 创建虚拟机 startVm
2. 注册 JNI 函数 startReg  准备 Java 所需要的 native 方法
3. 调用 `ZygoteInit.main`进入 Java 世界



进入 Java 世界的代码 如下：



<img src="http://ww1.sinaimg.cn/large/98900c07gw1fbgxhkg9l0j20gp0b1q4s.jpg"/>

<img src="http://ww4.sinaimg.cn/large/98900c07gw1fbgxih1cwnj20dg09575n.jpg"/>



代码注释：找到 ZygoteInit 调用它的 main 方法，并传入`com.android.internal.os.ZygoteInit`和`true`。

可见 **Java 世界的入口**是 `com.android.internal.os.ZygoteInit`的`main`函数。





## 小结



1. 创建第一个 Java 虚拟机
2. 创建 framework 核心 system_server 进程







