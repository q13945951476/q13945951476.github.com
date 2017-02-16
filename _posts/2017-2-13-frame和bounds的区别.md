---
layout: post
title: Frame和bounds的区别
---

<div class="message">
  frame和bounds虽然用过，但是都没有详细的了解过，特意到网上找找资料看看，顺变说一句，既然打算写文章，就好好写一写，网上找了很多，很多地方都是错的，看着直蒙圈啊，希望自己写的东西不至于误人子弟，参考文章链接就不贴出来，很多内容都是错的。自己照着网上内容，自己写代码运行，尝试出来的结论，贴出来看下，内容不多，仅做为自己的笔记，还请大神指点。
</div>

frame是当前view在父view中的位置和大小。
bounds是当前view自己的位置和大小，bounds的默认圆点是（0，0）可以使用setbounds修改。
frame的参照物是父view，bounds的参照物是自己。

<img src="/assets/2017/frame_bounds/000.png">

用demo验证一下
首先我们先设置view1的bounds是（25，25，200，200）。

{% highlight C %}
UIView *view1 = [[UIView alloc] initWithFrame:CGRectMake(50, 100, 200, 200)];
[view1 setBounds:CGRectMake(25, 25, 200, 200)];
view1.backgroundColor = [UIColor grayColor];
[self.view addSubview:view1];

UIView *view2 = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 100, 100)];
view2.backgroundColor = [UIColor redColor];
[view1 addSubview:view2];
{% endhighlight %}

<img src="/assets/2017/frame_bounds/111.png">

然后我们再设置view1的bounds是（-30，-30，200，200）。

<img src="/assets/2017/frame_bounds/222.png">

这有一个疑问，设置bounds的坐标系和正常view的坐标系不一样吗？不应该是原点坐标正数，是向右下角移动吗？负的原点坐标，不应该是向左上角移动吗？
设置frame就是（x，y）正数就向右下角移动啊。。到bounds这就反过来了呢？

我们将view1的bounds的后两个参数，设置大于frame的宽高，（-30，-30，240，240）.为什么显示是平均分配到四个方向了？不应该是根据原点坐标向x和y各延伸40吗？

<img src="/assets/2017/frame_bounds/333.png">

就是说假设view的frame是（50，50，150，150），然后设置frame（50，50，300，300）和bounds（0，0，300，300）显示的效果是不一样的，不，效果是一样的，位置是不一样的，难道是bounds的特性？

设置bounds对自身view没有影响，是影响已当前view为父视图（参照物）的子view。
