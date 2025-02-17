# gt3-android-sdk
# 本DEMO是带Button的验证码，如有需要请下载此demo和SDK
# 概述与资源

极验验证3.0 Android SDK提供给集成Android原生客户端开发的开发者使用。
集成极验验证3.0的时，需要先了解极验验证3.0的 [产品结构](http://docs.geetest.com/install/overview/#产品结构)。并且必须要先在您的后端搭建相应的**服务端SDK**，并配置从[极验后台]()获取的`<gt_captcha_id>`和`<geetest_key>`用来配置您集成了极验服务端sdk的后台。

# 安装

## 获取SDK

### 使用`git`命令从Github获取

```
git clone https://github.com/YanLingHao/Eclipse_sdk3.0-.git
```

### 手动下载获取

使用从github下载`.zip`文件获取最新的sdk。

[Github: gt3-android-sdk](https://github.com/YanLingHao/Eclipse_sdk3.0-.git)

## 手动导入SDK
从github上获取到`SDK`文件，同时将获取的`SDK`文件关联到您的项目中，并按照DEMO代码去集成。

## 初始化

### 在AndroidManifest.xml文件中添加权限
```java
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />

```
### 在对应的xml文件中添加控件并在代码中初始化

```java
    <com.example.sdk.GT3GeetestButton
        android:id="@+id/ll_btn_type"
        android:layout_width="290dp"
        android:layout_height="44dp"
        android:layout_centerHorizontal="true"
        android:layout_centerInParent="true"
        android:gravity="center"
        android:orientation="horizontal" />

```
```java
GT3GeetestButton gtbt=（GT3GeetestButton）findViewById(R.id.ll_btn_type);
```

### 设置服务端URL

| Attribute | Descripion |
| ------ | ------ |
| captchaURL|设置获取id，challenge，success的URL，需替换成自己的服务器URL|
|validateURL|设置二次验证的URL，需替换成自己的服务器URL|

```java
        new GT3GeetestUrl().setCaptchaURL(captchaURL);
        new GT3GeetestUrl().setValidateURL(validateURL);

```
### 注册GT3EventBus


```java

 compile 'org.greenrobot:eventbus:3.0.0'
```
### 验证码加载开始
```java
       gt3GeetestUtils = GT3GeetestUtils.getInstance(MainActivity.this);
        gt3GeetestUtils.getGeetest();

```

### 验证码加载的接口


```java
  
       gt3GeetestUtils.setGtListener(new GT3GeetestUtils.GT3Listener() {
            //拿到验证成功之后的结果
            @Override
            public void gt3GetDialogResult(String result) {

            }

            @Override
            public void gt3DialogSuccessResult(String result) {
                new Gt3GeetestTestMsg().setCandotouch(false);//这里设置验证成功后是否可以关闭
                Toast.makeText(getApplicationContext(), "这里是验证成功后执行的操作", Toast.LENGTH_SHORT).show();
            }
        });

```
