# 1、配置 Android Studio 的插件库来源
#### File->Settings->Plugins
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/150045666.png?imageslim)
#### 'Browse repositories...'->'Manage repositories...'
###### https://jcenter.bintray.com
###### 注意,需要先把 Android Studio 之前设置的 HTTP 代理去掉,否则打不开的.
###### 位置在 Settings 中第一项 Appearance &... 中 System Setting 下 HTTP Proxy,选 No proxy
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/162207252.png?imageslim)

# 2、搜索并安装 'Android ButterKnife Zelezny' 插件
#### 'Browse repositories...'
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/150553747.png?imageslim)

# 3、藉由插件生成代码
#### 在布局名上右键击鼠标，在弹出菜单中点按‘Generate...’项
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/162409870.png?imageslim)

#### 再次弹出列表中，会有 ‘Generate ButterKnife Injections’ 选项（非布局名称不会有此项）
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/152712036.png?imageslim)

#### 点按 ‘Generate ButterKnife Injections’ 选项，会弹出对话框，列出该布局中可用的元素 id 列表及操作选项
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/153824243.png?imageslim)

##### 初始如下
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/154027406.png?imageslim)

##### 生成后如下，其中 ①② 是自动生成的变量和事件定义代码，③ 是运行时将注解标记的 id 对应的UI元素实例赋给注解所在的变量引用上
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/154235377.png?imageslim)

##### 为了使上面的 ③ 能生效，需要引入编译时 ButterKnife 库依赖（在 app 模块的 build.gradle 中 dependencies 内添加）
###### compile 'com.jakewharton:butterknife:7.0.1'
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/154747283.png?imageslim)

## 总结
#### 一是 Android Studio 插件安装，以便根据布局自动生成变量及事件定义代码
#### 二是 库引入，据说是在编译时将 ButterKnife.bind(this); 和 @Bind 注解声明的变量 组合成常规的 "YYY xxx = findViewById(R.id.xxx); "
####
#### 最新[官方网站](http://jakewharton.github.io/butterknife/)描述 
###### '' compile 'com.jakewharton:butterknife:8.5.1' ''
###### '' annotationProcessor 'com.jakewharton:butterknife-compiler:8.5.1' ''
###### 此时插件生成的 @Bind 已经在 8.5.1 中不存在，由 @BindView 替代即可。
###
###### 8.5.1 中的注解列表如下：
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/161716576.png?imageslim)


## 随想
#### 折腾一大圈儿，只是将 findViewById 这一部分隐藏到编译时生成，相对来说更隐晦了。
#### 倒不如同样用插件，生成 ViewHolder 内部类定义于 Activity,并赋于Activity变量 ViewHolder viewHolder;
#### 那么完整的过程，由合理的布局支撑，原有的代码仅由 Android Studio 插件自动生成，即可解决一切，回归原始。
##
## 参考自动生成代码
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/171525390.png?imageslim)

## 而该 ViewHolder 独立成如 Visual C# 相似的分步类，将业务与UI分离，可能也不错吧
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/172422819.png?imageslim)

## 世界变得如此清静，依旧还是布局名称上面右击弹出列表选择布局中的界面元素。
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/172804509.png?imageslim)

## 同理，还有一个 Service 需要从 Activity 中独立出来
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/174001748.png?imageslim)

## 至此，一个 Activity，两个附属类 Presenter 和 Service,各自持有 Activity 引用，
## Activity 中注册 Presenter 和 Service 对各自事件的回调方法，在 Activity 中决定下一步事件流向处理。
## Activity 从此作为 Controller,回归流控的作用，而非界面呈现或数据加工的集散地。
## 业务与呈现的进一步功能缩进，确保了 Activity 专注于流控功能
## 至于适配器是否需要引入，以解决部分流控标志性数据加工,还是根据实际需要再定吧。
