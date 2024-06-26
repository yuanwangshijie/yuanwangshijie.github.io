# CSS3毛玻璃效果


## backdrop-filter与filter的区别

> filter：模糊内容<br>
> backdrop-filter:透过该层的底部元素模糊化<br>
> 这两个属性的语法是一样的

**下面是使用案例**<br>

``` css
backdrop-filter:saturate(150%) contrast(50%) blur(8px);
background-color:rgba(0,0,0,.3);
```

saturate(150%)意为使…饱和，类似ps饱和度效果，小于100%变暗，大于100%变亮<br>
contrast(50%)意为对比，类似ps对比度，100%为原图，0%为全灰色图像

