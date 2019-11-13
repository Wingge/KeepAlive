# 干啥用的

这是一个让android程序尽量存活的项目。

由于工作需要，我的应用基本都需要做保活，有单进程保活的，有双进程的（这个得看环境，如果能直接把两个或多个应用同时安装到用户机器上即可使用多进程方案）。

这下面有两个比较好的保活总结：

https://juejin.im/entry/58acf391ac502e007e9a0a11

https://juejin.im/post/5baedde6f265da0a8d369eb2

这些文章说的都还算比较全面的。

我这里实现是这样的：双进程aidl互相绑定，断开拉起对方。单进程使用广播自我守护，并通过前台服务提交进程优先级以避免被系统回收。前台服务通知作了隐藏（8.0以下）以避免用户反感卸载。锁屏后会启用1像素Activity以提高存活能力，开屏后销毁。

# 效果

7.0以下完美,无法停止任一进程。这边测试有oppo，华为，几种山寨机

8.0，9.0看机型，目前我手上的三星是完美的。华为测试可以去设置停止运行。

机型太少，具体大家看着办吧，7.0应该还是效果杠杠的。

# 如何使用

1.先克隆看效果：git clone https://github.com/Wingge/KeepAlive.git --recursive

2.其中ProtectService，独立一个程序（需修改client的包名及client服务类全名）

3.ProtectClient代码拷到自己开发的程序中（需注意前台服务channel,channnelName,notificationId不要和ProtectService一样，避免冲突）。

4.如果你的程序有开屏UI，可以替换OnePiexlActivity作为开屏前台UI.

