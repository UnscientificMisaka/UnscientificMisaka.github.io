---
layout:     post
title:      "蓝牙开发"
subtitle:    "关于安卓6.0广播问题"
date:       2016-11-11 14:24:00
author:     "LRZ"
header-img: "img/post-bg-第一篇.jpg"
tags:
    - Android
---
## 蓝牙
一直接收不到搜索到设备的广播，自己一个人瞎琢磨也不知道哪里出了问题，百度的情况也没用上，看了看API文档也没找到问题。留着日后更上解决方法，![](http://i.imgur.com/CMeC8IC.png)
![](http://i.imgur.com/1px7v4v.png)<br>
11月13日update：<br>
安卓6.0要动态添加权限！<br>
安卓6.0权限系统大改，不在一开始安装时给与app权限，而是动态申请。同时还要另外添加android.permission.ACCESS_COARSE_LOCATION和ACCESS_fINE_LOCATION"。换个低版本的安卓手机一点问题都没有。心酸踩坑里浪费这么久的时间，吸取教训要多逛逛Stackoverflow。<br>
```
if (Build.VERSION.SDK_INT >= 6.0) {
    if(ActivityCompat.checkSelfPermission(this,Manifest.permission.ACCESS_COARSE_LOCATION)!=PackageManager.PERMISSION_GRANTED){
        /**动态添加权限：ACCESS_FINE_LOCATION*/
        ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.ACCESS_FINE_LOCATION},
            MY_PERMISSION_REQUEST_CONSTANT);
        }
    }
```
<br>然后函数回调
```
public void onRequestPermissionsResult(int requestCode, String permissions[], int[] grantResults) {
    switch (requestCode) {
        case MY_PERMISSION_REQUEST_CONSTANT: {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                Log.i("testFindDevice","添加权限成功");
            }
        return;
        }
    }
}  
```