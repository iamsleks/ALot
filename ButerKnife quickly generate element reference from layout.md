# 1、配置 Android Studio 的插件库来源
## File->Settings->Plugins
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/150045666.png?imageslim)
## 'Browse repositories...'->'Manage repositories...'
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/150215082.png?imageslim)

# 2、搜索并安装 'Android ButterKnife Zelezny' 插件
## 'Browse repositories...'
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/150553747.png?imageslim)

# 3、藉由插件生成代码
## 在布局名上右键击鼠标，在弹出菜单中点按‘Generate...’项
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/151147099.png?imageslim)

## 再次弹出列表中，会有 ‘Generate ButterKnife Injections’ 选项（非布局名称不会有此项）
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/152712036.png?imageslim)

## 点按 ‘Generate ButterKnife Injections’ 选项，会弹出对话框，列出该布局中可用的元素 id 列表及操作选项
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/153824243.png?imageslim)

## 初始如下
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/154027406.png?imageslim)

## 生成后如下，其中 ①② 是自动生成的变量和事件定义代码，③ 是运行时将注解标记的 id 对应的UI元素实例赋给注解所在的变量引用上
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/154235377.png?imageslim)

## 为了使上面的 ③ 能生效，需要引入编译时 ButterKnife 库依赖（在 app 模块的 build.gradle 中 dependencies 内添加）
### compile 'com.jakewharton:butterknife:7.0.1'
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/154747283.png?imageslim)

## 总结
### 一是 Android Studio 插件安装，以便根据布局自动生成变量及事件定义代码
### 二是 库引入，据说是在编译时将 ButterKnife.bind(this); 和 @Bind 注解声明的变量 组合成常规的 "YYY xxx = findViewById(R.id.xxx); "
###
### 最新[官方网站](http://jakewharton.github.io/butterknife/)描述 
### '' compile 'com.jakewharton:butterknife:8.5.1' ''
### '' annotationProcessor 'com.jakewharton:butterknife-compiler:8.5.1' ''
### 此时插件生成的 @Bind 已经在 8.5.1 中不存在，由 @BindView 替代即可。
###
### 8.5.1 中的注解列表如下：
![mark](http://oo30yo29t.bkt.clouddn.com/blog/20170501/161716576.png?imageslim)

