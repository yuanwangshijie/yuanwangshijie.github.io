# 随机图片api


## 一、api整合

### 樱道

> 网站：https://img.r10086.com/

* 调用地址：
* 二次元动漫(1-18)：https://api.r10086.com/img-api.php?type=动漫综合1
* 东京食尸鬼(横竖屏)：https://api.r10086.com/img-api.php?type=东京食尸鬼横屏系列1
* Fate(横竖屏)：https://api.r10086.com/img-api.php?type=Fate横屏系列1
* 为美好世界献上祝福(横竖屏)：https://api.r10086.com/img-api.php?type=为美好世界献上祝福横屏系列1
* 某科学的超电磁炮(横竖屏)：https://api.r10086.com/img-api.php?type=某科学的超电磁炮横屏系列1
* 原神(横竖屏)：https://api.r10086.com/img-api.php?type=原神横屏系列1
* 我的世界：https://api.r10086.com/img-api.php?type=我的世界系列1
* 神奇宝贝(横竖屏)：https://api.r10086.com/img-api.php?type=神奇宝贝横屏系列1
* 龙珠(横竖屏)：https://api.r10086.com/img-api.php?type=龙珠横屏系列1
* 罪恶王冠(横竖屏)：https://api.r10086.com/img-api.php?type=罪恶王冠横屏系列1
* 鬼灭之刃(横竖屏)：https://api.r10086.com/img-api.php?type=鬼灭之刃横屏系列1
* 火影忍者(横竖屏)：https://api.r10086.com/img-api.php?type=火影忍者横屏系列1
* 海贼王(横竖屏)：https://api.r10086.com/img-api.php?type=海贼王横屏系列1
* 进击的巨人(横竖屏)：https://api.r10086.com/img-api.php?type=进击的巨人横屏系列1
* 从零开始的异世界生活(横竖屏)：https://api.r10086.com/img-api.php?type=从零开始的异世界生活横屏系列1
* 刀剑神域(横竖屏)：https://api.r10086.com/img-api.php?type=刀剑神域横屏系列1
* 钢之炼金术师(横竖屏)：https://api.r10086.com/img-api.php?type=钢之炼金术师横屏系列1
* 妖精的尾巴(横竖屏)：https://api.r10086.com/img-api.php?type=妖精的尾巴横屏系列1
* 缘之空(横竖屏)：https://api.r10086.com/img-api.php?type=缘之空横屏系列1
* 东方project：https://api.r10086.com/img-api.php?type=东方project1
* 猫娘：https://api.r10086.com/img-api.php?type=猫娘1
* 风景(1-10)：https://api.r10086.com/img-api.php?type=风景系列1
* 物语(1-2)：https://api.r10086.com/img-api.php?type=物语系列1
* 少女前线：https://api.r10086.com/img-api.php?type=少女前线1
* 明日方舟(1-2)：https://api.r10086.com/img-api.php?type=明日方舟1
* 重装战姬：https://api.r10086.com/img-api.php?type=重装战姬1
* P站(1-4)：https://api.r10086.com/img-api.php?type=P站系列1
* CG(1-5)：https://api.r10086.com/img-api.php?type=CG系列1
* 守望先锋：https://api.r10086.com/img-api.php?type=守望先锋
* 王者荣耀：https://api.r10086.com/img-api.php?type=王者荣耀
* 少女写真(1-6)：https://api.r10086.com/img-api.php?type=少女写真1
* 死库水萝莉：https://api.r10086.com/img-api.php?type=死库水萝莉
* 萝莉：https://api.r10086.com/img-api.php?type=萝莉
* 极品美女图片：https://api.r10086.com/img-api.php?type=极品美女图片
* 日本COS中国COS：https://api.r10086.com/img-api.php?type=日本COS中国COS
* 橘里橘气(横竖屏)：https://api.r10086.com/img-api.php?type=橘里橘气横屏系列1

### 保罗

> 网站：https://api.paugram.com/help/wallpaper

* 调用地址：https://api.paugram.com/wallpaper/

### 东方Project

* 调用地址：https://img.paulzzh.com/touhou/random

### likepoems随机图

> 网站：https://api.likepoems.com/

* 调用地址：
* 二次元PC壁纸：https://api.likepoems.com/img/pc
* 二次元PE壁纸：https://api.likepoems.com/img/pe
* mc酱壁纸：https://api.likepoems.com/img/mc
* pixiv壁纸：https://api.likepoems.com/img/pixiv
* nature壁纸：https://api.likepoems.com/img/nature
* 必应壁纸：https://api.likepoems.com/img/bing


## 二、怎么自制随机图

1. 准备图片—>书写路径—>书写php文件
2. 在img文件夹里新建img.txt，文件中直接写图片的URL地址，如：

```
https://static.likepoems.com/2020/10/06/385ea1c4c8b4fbac57f5a0aa61f033761.jpg
https://static.likepoems.com/2021/06/12/20210126104630786.png
```

3. 新建index.php文件。文件内容如下：

``` php
<?php
//存放api随机图链接的文件名img.txt
$filename = "img.txt";
if(!file_exists($filename)){
    die('文件不存在');
}

//从文本获取链接
$pics = [];
$fs = fopen($filename, "r");
while(!feof($fs)){
    $line=trim(fgets($fs));
    if($line!=''){
        array_push($pics, $line);
    }
}

//从数组随机获取链接
$pic = $pics[array_rand($pics)];

//返回指定格式
$type=$_GET['type'];
switch($type){

//JSON返回
case 'json':
    header('Content-type:text/json');
    die(json_encode(['pic'=>$pic]));

default:
    die(header("Location: $pic"));
}
?>
```

4. 然后放在服务器里面的api文件夹里，绑定域名，记得开启php环境
5. 访问路径：你的域名/api/img

