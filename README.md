# 空祖家的对话框 2.0
献给要求我们安卓照着苹果设计稿做开发的产品们（手动滑稽

<a href="https://github.com/kongzue/Dialog/">
<img src="https://img.shields.io/badge/Kongzue%20Dialog-2.0.3-green.svg" alt="Kongzue Dialog">
</a> 
<a href="https://bintray.com/myzchh/maven/dialog/2.0.3/link">
<img src="https://img.shields.io/badge/Maven-2.0.3-blue.svg" alt="Maven">
</a> 
<a href="http://www.apache.org/licenses/LICENSE-2.0">
<img src="https://img.shields.io/badge/License-Apache%202.0-red.svg" alt="Maven">
</a> 
<a href="http://www.kongzue.com">
<img src="https://img.shields.io/badge/Homepage-Kongzue.com-brightgreen.svg" alt="Maven">
</a> 

空祖家的对话框2.0拥有提供最简单的调用方式以实现消息框、选择框、输入框、等待提示、警告提示、完成提示、错误提示等弹出样式。以下是目前包含的所有对话框样式预览图：

![Kongzue's Dialog](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.0.png)

试用版可以前往 http://kongzue.com/open_source/KongzueDialogDemo2.0.apk 下载

![Kongzue's Dialog Demo](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/KongzueDialogDemoDownload.png)

本例中，包含DialogDemo（Dialog/app/）是对话框的演示项目源代码，以及Library库（Dialog/dialog/）是封装的空祖家对话框的源代码。

项目托管的Maven仓库在https://bintray.com/myzchh/maven/dialog

本项目遵循Apache-2.0开源协议，具体可参考：http://www.opensource.org/licenses/apache2.0.php

## Maven仓库或Gradle的引用方式
Maven仓库：
```
<dependency>
  <groupId>com.kongzue.dialog</groupId>
  <artifactId>dialog</artifactId>
  <version>2.0.4</version>
  <type>pom</type>
</dependency>
```
Gradle：
在dependencies{}中添加引用：
```
implementation 'com.kongzue.dialog:dialog:2.0.4'
```

## 使用说明
1) 组件启用前请先初始化全局的风格样式，具体方法为
```
DialogSettings.type = TYPE_MATERIAL;
```

Material 风格对应 DialogSettings.TYPE_MATERIAL，

Kongzue 风格对应 DialogSettings.TYPE_KONGZUE，

iOS 风格对应 DialogSettings.TYPE_IOS

需要注意的是风格设置仅针对对话框，提示框样式不会改变。

2) 要启用 Light & Dark 黑白主题模式，请调用以下语句实现：
```
DialogSettings.tip_theme = THEME_LIGHT;         //设置提示框主题为亮色主题
DialogSettings.dialog_theme = THEME_DARK;       //设置对话框主题为暗色主题
```

具体预览图如下：
![Kongzue's Dialog Light&DarkMode](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.0_dark.png)

3) 从2.0.4版本开始，提供不需要悬浮窗权限，且可以跨域显示的通知功能，如下图所示：
![Kongzue's Dialog Light&DarkMode](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.0.4_notification.png)

## 关于v2组件包
在空祖家的对话框组件中，依然保留了一代的组件库但不再推荐使用，这是为了保持兼容性，若强行使用您会看到相关类的名称上有删除线。

为了更有效率的开发，我们现在强烈推荐直接使用v2组件库，其包含的包地址为：com.kongzue.dialog.v2

### 调用消息对话框的方法：
```
MessageDialog.show(me, "消息提示框", "用于提示一些消息", "知道了", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
    }
});
```
或者可以采用快速调用方式：
```
MessageDialog.show(me, "欢迎", "欢迎使用Kongzue家的对话框，此案例提供常用的几种对话框样式。\n如有问题可以在https://github.com/kongzue/Dialog提交反馈");
```

### 调用选择对话框的方法：
```
SelectDialog.show(me, "提示", "请做出你的选择", "确定", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        Toast.makeText(me, "您点击了确定按钮", Toast.LENGTH_SHORT).show();
    }
}, "取消", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        Toast.makeText(me, "您点击了取消按钮", Toast.LENGTH_SHORT).show();
    }
});
```
或者可以采用快速调用方式：
```
SelectDialog.show(me, "提示", "请做出你的选择", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        Toast.makeText(me, "您点击了确定按钮", Toast.LENGTH_SHORT).show();
    }
});
```

### 调用输入对话框：
```
InputDialog.show(me, "设置昵称", "设置一个好听的名字吧", "确定", new InputDialogOkButtonClickListener() {
    @Override
    public void onClick(Dialog dialog, String inputText) {
        Toast.makeText(me, "您输入了：" + inputText, Toast.LENGTH_SHORT).show();
    }
}, "取消", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

    }
});
```
或者可以采用快速调用方式：
```
InputDialog.show(me, "设置昵称", "设置一个好听的名字吧", new InputDialogOkButtonClickListener() {
                    @Override
                    public void onClick(Dialog dialog, String inputText) {
                        Toast.makeText(me, "您输入了：" + inputText, Toast.LENGTH_SHORT).show();
                    }
                });
```

### 调用等待提示框：
```
WaitDialog.show(me, "载入中...");
```

### 调用完成提示框：
```
TipDialog.show(me, "完成", TipDialog.SHOW_TIME_SHORT, TipDialog.TYPE_FINISH);
```

### 调用警告提示框：
```
TipDialog.show(me, "请输入密码", TipDialog.SHOW_TIME_SHORT, TipDialog.TYPE_WARNING);
```

### 调用错误提示框：
```
TipDialog.show(me, "禁止访问", TipDialog.SHOW_TIME_LONG, TipDialog.TYPE_ERROR);
```

### 调用消息通知：

注意，此处使用的是来自com.kongzue.dialog.v2的Notification类。

通知消息（v2.Notification）与提示框（v2.TipDialog）的主要区别是提示框会打断用的操作，而消息通知不会，消息通知适合于并发需要提醒用户是否处理消息的业务场景，而提示框适用于阻断用户操作，提醒用户当前发生的情况的业务场景。

```
Notification.show(me, id, iconResId, getString(R.string.app_name), "这是一条消息", Notification.SHOW_TIME_LONG, notifactionType)
                        .setOnNotificationClickListener(new Notification.OnNotificationClickListener() {
                            @Override
                            public void OnClick(int id) {
                                Toast.makeText(me,"点击了通知",SHOW_TIME_SHORT).show();
                            }
                        })
                ;
```
其中，id为通知消息id，在用户点击该通知后，会在OnNotificationClickListener中进行回调。

字段 | 含义 | 是否必须
---|---|---
context | 上下文索引 | 必须
iconResId | 图标 | 可选
title | 通知标题 | 可选
message | 通知内容 | 必须
notifactionType | 消息类型 | 必须
OnNotificationClickListener | 下载监听器 | 可选

注意，此处的消息类型 notifactionType 目前仅对“Kongzue 风格”有效，且提供的风格有：

字段 | 含义 | 是否默认
---|---|---
TYPE_NORMAL | 默认灰黑色 | 默认
TYPE_FINISH | 绿色 | 可选
TYPE_WARNING | 橙色 | 可选
TYPE_ERROR | 红色 | 可选

另外，可以采用快速调用方式：
```
Notification.show(me, 0, "", "这是一条消息", Notification.SHOW_TIME_SHORT, notifactionType);
```

## 附加功能：
在任何一种对话框中都可以使用.setCanCancel(boolean)来设置是否可以点击对话框以外的区域关闭对话框，提示类默认都是禁止的，选择、输入对话框默认也是禁止的，消息对话框默认是允许的。

使用方法可以参考以下代码：
```
WaitDialog.show(me, "载入中...").setCanCancel(true);
```

在空祖家的对话框组件中，您可以使用监听器来监听对话框的生命周期，Demo如下：
```
WaitDialog.show(me, "载入中...").setCanCancel(true).setDialogLifeCycleListener(new DialogLifeCycleListener() {
    @Override
    public void onCreate(AlertDialog alertDialog) {
        //此时对话框创建
    }
    @Override
    public void onShow(AlertDialog alertDialog) {
        //此时对话框显示
    }
    @Override
    public void onDismiss() {
        //此时对话框关闭
    }
});
```

另外提供一些定制属性：
```
DialogSettings.dialog_title_text_size = -1;     //设置对话框标题文字大小，<=0不启用
DialogSettings.dialog_message_text_size = -1;   //设置对话框内容文字大小，<=0不启用
DialogSettings.dialog_button_text_size = -1;    //设置对话框按钮文字大小，<=0不启用
DialogSettings.tip_text_size = -1;              //设置提示框文字大小，<=0不启用
DialogSettings.ios_normal_button_color = -1;    //设置iOS风格默认按钮文字颜色，=-1不启用
```

## 开源协议
```
   Copyright Kongzue Dialog

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
```

## 更新日志：
v2.0.4:
- 提供消息与通知功能；

v2.0.3:
- 提供部分文字大小和颜色修改；

v2.0.2:
- 提供Light和Dark两种黑白主题模式；

v2.0.1:
- TipDialog提供自定义提示图标；
- WaitDialog可通过dismiss()方法关闭等待提示框；

v2.0.0:
- 新增v2组件库；
