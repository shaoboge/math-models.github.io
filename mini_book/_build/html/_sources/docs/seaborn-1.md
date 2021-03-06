---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.12
    jupytext_version: 1.6.0
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

+++ {"slideshow": {"slide_type": "slide"}, "id": "CB540DCA177742AD8DA0CFC1092B7ECB", "mdEditEnable": false, "jupyter": {}, "tags": []}

# Seaborn-1

## seaborn 简介


**Seaborn是一种基于matplotlib**的图形可视化python library。它提供了一种高度交互式界面，便于用户能够做出各种有吸引力的统计图表。

Seaborn其实是在**matplotlib的基础上进行了更高级的API封装**，从而使得作图更加容易，在大多数情况下使用seaborn就能做出很具有吸引力的图，而使用matplotlib就能制作具有更多特色的图。

**应该把Seaborn视为matplotlib的补充，而不是替代物。** 同时它能高度兼容numpy与pandas数据结构以及scipy与statsmodels等统计模式。掌握seaborn能很大程度帮助我们更高效的观察数据与图表，并且更加深入了解它们。


其有如下特点：

- 基于matplotlib aesthetics绘图风格，增加了一些绘图模式
- 增加调色板功能，利用色彩丰富的图像揭示您数据中的模式
- 运用数据子集绘制与比较单变量和双变量分布的功能
- 运用聚类算法可视化矩阵数据
- 灵活运用处理时间序列数据
- 利用网格建立复杂图像集


官方网站：http://seaborn.pydata.org
在接下来的一段时间内，我们将带大家深入地了解各类seaborn绘图函数。


## 使用散点图发现数据之间的关联



散点图是数据可视化中最常用的图像。它直观地向我们展示了数据之间的分布关系，如果数据之间存在线性或者其他相关关系，很容易通过散点图观察出来。



除了之前提到的`plt.scatter()`，使用seaborn也可以绘制散点图。对用的命令是`scatterplot()`

```{code-cell} ipython3
---
id: 8290A85D21DA4EB38856D39D5639D7DE
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns  # 导入 seaborn 并且命名为sns
sns.set(style="darkgrid") # 设置绘图格式为darkgrid
```

```{code-cell} ipython3
---
id: 6F64139BA8AF441A8FB970231B5C0A65
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
tips = sns.load_dataset('tips')
```

```{code-cell} ipython3
---
id: A73C71D946034B68859FF46C0EA6F711
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
#tips = pd.read_csv("../_static/lecture_specific/seaborn/tips.csv")

```

```{code-cell} ipython3
---
id: D28E24365D3A4B0CBFDBBEB57C980356
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
tips.head() # 查看数据的前五行



```


```{code-cell} ipython3
---
id: E13205EA136A4F3E8025C1CC6293B45A
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
plt.scatter(tips['total_bill'],tips['tip']) # 使用plt.scatter 方法绘制两列数据的散点图
plt.xlabel('Total bill')
plt.ylabel('tip')
```

```{code-cell} ipython3
---
id: 522F6FC1BB254D54B0C3CE9AED7F1454
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.scatterplot(tips.total_bill,tips.tip) # 使用sns.scatterplot 方法绘制两列数据的散点图
plt.xlabel("Total Bill")
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "E6C4B1AF25604EB481E23A341B85261C", "mdEditEnable": false, "jupyter": {}, "tags": []}

除此之外，我们还可以通过在 `relplot()`中指定`kind="scatter"`获取同样的效果。

```{code-cell} ipython3
---
id: F0431262CCB847798DB8C0E7C62B3886
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
# sns.relplot(x="total_bill", y="tip", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "648FCFBD55C246BB86272F1872F66415", "mdEditEnable": false, "jupyter": {}, "tags": []}

相比于`scatterplot`，`relplot`的集成度更高，在使用方法上也更为方便。例如，如果我们想给散点图加上第三个维度，就直接可以通过一个参数`hue`进行传递即可。该参数将会给不同的类别赋以不同的颜色。

```{code-cell} ipython3
---
id: 69BEE2B1A9D04008BDDCB744B5F071A8
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
# sns.relplot(x="total_bill", y="tip", hue="smoker", data=tips)
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "BF60077D690649FCAAE048BDEFC01FE7", "mdEditEnable": false, "jupyter": {}, "tags": []}

除此之外，我们还可以继续修改散点的形状，只需要引入`style`参数

```{code-cell} ipython3
---
id: 0A0F415DEEF94D6E9B7F1440637612AD
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="total_bill", y="tip", hue="smoker", style="sex",data=tips)
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "651BF6FB4BC74B99AD9FEA2388359352", "mdEditEnable": false, "jupyter": {}, "tags": []}

结合`hue`和`style`两个参数，我们就可以实现四维数据的绘图。需要注意的是，人眼的形状的敏感性不如颜色，因此该方法应该慎用，因为第四个维度不容易被观察到。

```{code-cell} ipython3
---
id: 778A160BD2D14B4D93DA6E3D79D7ABE3
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="total_bill", y="tip", hue="smoker", style="time", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "4A2294095658483A97E1984FA94473E9", "mdEditEnable": false, "jupyter": {}, "tags": []}

在上面的案例中，`hue`参数接受到的是离散的类别数据，而如果我们给它传入一个数值形式的数据，那么`relplot`将会用连续变化的色谱来区分该数据。

```{code-cell} ipython3
---
id: F4C0468959A24402B29B975B87351D17
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="total_bill", y="tip", hue="size", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "4F11101CA1E84A4F8EC87D6CBE80EBCF", "mdEditEnable": false, "jupyter": {}, "tags": []}

当然了，除了散点的颜色的形状，我们还可以修改散点的大小，只需要指定`size`参数即可。



```{code-cell} ipython3
---
id: 624A565439044F19BD99E19BEEC14BD8
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="total_bill", y="tip", size="size", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "577985F1BFE2445C9F31866C039CF945", "mdEditEnable": false, "jupyter": {}, "tags": []}

下面是一个综合使用以上参数，得到的一个五维的散点图。


```{code-cell} ipython3
---
id: 65CB6C348E0C441B90B06360107166E0
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="total_bill", y="tip", hue='sex',
            style = 'time',size="size", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "499F1D55AFD54A3A898E9651C607B918", "mdEditEnable": false, "jupyter": {}, "tags": []}





## 数据的汇总和不确定性的展示

```{code-cell} ipython3
---
id: A7150C95BFB9422F94A79CC4393F82F5
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
fmri = sns.load_dataset("fmri")
# fmri = pd.read_csv("/home/kesci/input/Seaborn_Demo6897/fmri.csv")
fmri.head()
```

```{code-cell} ipython3
---
id: 6BCED1AA76684B49AEDEAA13280CDCC0
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="timepoint", y="signal", kind="line", data=fmri);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "E9398B8C222E42F197F8F1D76175CF3B", "mdEditEnable": false, "jupyter": {}, "tags": []}

此外，不确定度还可以用标准差来衡量，只需要设置`ci='sd'`即可

```{code-cell} ipython3
---
id: D042094D43C8417AB046F69E4ECFD84B
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="timepoint", y="signal", kind="line", ci="sd", data=fmri);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "F680F6A5738B4E8483A8996E3AF866ED", "mdEditEnable": false, "jupyter": {}, "tags": []}

如果我们关掉数据汇总，那么绘制出来的图像会非常奇怪。这是因为在某一个时间，会有多个测量数据。

```{code-cell} ipython3
---
id: 2C5534B7D533421F982F8B3DB027E80D
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="timepoint", y="signal", estimator=None, kind="line", data=fmri);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "1C0359CBCD864EB49B5D40BDA38EAB39", "mdEditEnable": false, "jupyter": {}, "tags": []}

## 绘制子数据集

+++ {"slideshow": {"slide_type": "slide"}, "id": "A126BFD5C7F449F89D144C9A14DD3247", "mdEditEnable": false, "jupyter": {}, "tags": []}

同`scatterplot()`一样，我们可以通过修改`hue`,`style`,`size`,来增加更多的绘图维度，用法也是非常一致的，这意味着我们可以非常简单地在两种方法之间进行替换。

+++ {"slideshow": {"slide_type": "slide"}, "id": "16A69880647C429592C11A9948A140A5", "mdEditEnable": false, "jupyter": {}, "tags": []}

例如，如果我们引入`hue`参数，对event进行分类。即可得到如下的数据汇总图。

```{code-cell} ipython3
---
id: 2126366D46D64623B2B8A851F42D57A3
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="timepoint", y="signal", hue="event", kind="line", data=fmri);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "A47BF8B3CD714922ACE8292925888B93", "mdEditEnable": false, "jupyter": {}, "tags": []}

我们继续加入另一个`style`参数，可以把region也考虑进去。

```{code-cell} ipython3
---
id: C77AA3FD3607484989E74D6380C62992
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="timepoint", y="signal", hue="region", style="event",
            kind="line", data=fmri);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "9DB7451053964B5CA80167D4E27E5352", "mdEditEnable": false, "jupyter": {}, "tags": []}

为了突出显示，我们还可以修改线型。

```{code-cell} ipython3
---
id: 8A4108F4575D415881BC488881EE2FA7
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="timepoint", y="signal", hue="region", style="event",
            dashes=False, markers=True, kind="line", data=fmri);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "13B5E986599C4E42813EDF5453391EE7", "mdEditEnable": false, "jupyter": {}, "tags": []}

下面我们考虑另一个数据集

```{code-cell} ipython3
---
id: 15A81F3451E2476A850374B5F01BD0D6
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
dots = sns.load_dataset("dots").query("align == 'dots'")

# dots = pd.read_csv('/home/kesci/input/Seaborn_Demo6897/dots.csv',encoding = 'utf-8')
# dots = dots[dots["align"] == 'dots']
dots.head()
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "1935E3AB386E40B2AE1205E7E328FB92", "mdEditEnable": false, "jupyter": {}, "tags": []}

上面的例子我们用的是离散变量作为参数`hue`和`chioce`的值，实际上，他们也可以使用连续变量。比如下面的例子

```{code-cell} ipython3
---
id: 9EB368EBA4E5457E8F6C661344FB963F
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="time", y="firing_rate",
            hue="coherence", style="choice",
            kind="line", data=dots);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "83CD40E88D4A4FCA806392DE5AF7C67C", "mdEditEnable": false, "jupyter": {}, "tags": []}

请注意，当`style`的可能性增多时，肉眼可能不太能够区分不同的线型，因此该方法需要在变量取值范围较小的情况下使用。

```{code-cell} ipython3
---
id: 2D88715ACE7D46D1A00D4CB2A23DC68B
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
palette = sns.cubehelix_palette(light=.8, n_colors=6)
sns.relplot(x="time", y="firing_rate",
           hue="coherence", size="choice",
           palette=palette,
           kind="line", data=dots);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "AF3B8E0E1E764CD4A913E48E7F39BE3A", "mdEditEnable": false, "jupyter": {}, "tags": []}


## 使用多张图展示数据之间的相互关系

+++ {"slideshow": {"slide_type": "slide"}, "id": "64068B276E284DD0A82231077A289C4E", "mdEditEnable": false, "jupyter": {}, "tags": []}

下面我们学习如何使用多张子图，分析与展示数据之间的相关性。使用的参数主要是`col`

```{code-cell} ipython3
---
id: 23D0FB43281A4CA4A6F22167FB346633
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="total_bill", y="tip", hue="smoker",
            col="time", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "1870567DD1164080A29137878F7F19E0", "mdEditEnable": false, "jupyter": {}, "tags": []}

此外，我们还可以通过`row`参数，进一步地扩大子图的规模

```{code-cell} ipython3
---
id: 4CE6CFA00EA04DB19E9269B4098C8AE2
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="total_bill", y="tip", hue="smoker",
            col="time",row = 'sex', data=tips);
```

```{code-cell} ipython3
---
id: E3E2C8C8BF0944AB9F3C575302E2C107
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.relplot(x="timepoint", y="signal", hue="subject",
            col="region", row="event", height=4,
            kind="line", estimator=None, data=fmri);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "D1C202C5CBA746209CAD5F00C68C4A6F", "mdEditEnable": false, "jupyter": {}, "tags": []}

以上的一系列可视化方法，称为小倍数绘图（ “lattice” plots or “small-multiples”），在研究大规模数据集的时候尤为重要，因为使用该方法，可以把复杂的数据根据一定的规律展示出来，并且借助可视化，使人的肉眼可以识别这种规律。


需要注意的是，有的时候，简单的图比复杂的图更能帮助我们发现和解决问题。

+++ {"id": "DE93A9F7B3634D20976A0E64EDC55AE6", "jupyter": {}, "tags": [], "slideshow": {"slide_type": "slide"}, "mdEditEnable": false}

**课堂练习**

使用iris数据集，进行数据可视化。要求以`sepal_length`为横轴，以`sepal_width`为纵轴，以花的种类为颜色标准，绘制散点图。你可以使用如下的代码导入iris数据集。

```{code-cell} ipython3
---
id: C47E5532FBA541D8ACBEC85D5FC30566
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
iris = sns.load_dataset('iris')
```

```{code-cell} ipython3
---
id: 94B6CBD5D63349C0883C9C929556C8DB
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
# your code here
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "2E9FC476F8DB4C64BBB350B97D4A2940", "mdEditEnable": false, "jupyter": {}, "tags": []}


## 绘制离散形式的变量

+++ {"slideshow": {"slide_type": "slide"}, "id": "42270275DCC0424E909C73E5B663D9CF", "mdEditEnable": false, "jupyter": {}, "tags": []}

在上一节中，我们学习了如何使用`relplot()`描述数据集中多变量之间的关系，其中我们主要关心的是两个数值型变量之间的关系。本节我们进一步地，讨论离散型（ categorical）变量的绘制方法。

+++ {"slideshow": {"slide_type": "slide"}, "id": "7216109EDC9A4C389F92AFAD51CC94D1", "mdEditEnable": false, "jupyter": {}, "tags": []}

在seaborn中，我们有很多可视化离散型随机变量的方法。类似于`relplot()`之于`scatterplot()` 和 `lineplot()`的关系, 我们有一个`catplot()`方法，该方法提高了我们一个从更高层次调用各类函数的渠道，例如`swarmplot()`,`boxplot()`,`violinplot()`等。

+++ {"slideshow": {"slide_type": "slide"}, "id": "814228AB7753435C86ACB8D5736EFDD9", "mdEditEnable": false, "jupyter": {}, "tags": []}

在详细地学习这些方法之前，对他们做一个系统地分类是非常有必要的，他们按照绘制内容可以分成如下三类：

+++ {"slideshow": {"slide_type": "slide"}, "id": "F4904105EA5A48FE84269D30AB2D9D3B", "mdEditEnable": false, "jupyter": {}, "tags": []}

- Categorical **scatterplots:**
    * `stripplot()` (with kind="strip"; the default)
    * `swarmplot()` (with kind="swarm")
    
- Categorical **distribution plots:**
    * `boxplot()` (with kind="box")
    * `violinplot()` (with kind="violin")
    * `boxenplot()` (with kind="boxen")
- Categorical **estimate plots:**
    * `pointplot()` (with kind="point")
    * `barplot()` (with kind="bar")
    * `countplot()` (with kind="count")

+++ {"slideshow": {"slide_type": "slide"}, "id": "6AE0EB545AE94C5DAC60959F67AB1C62", "mdEditEnable": false, "jupyter": {}, "tags": []}

以上三个类别代表了绘图的不同角度，在实践中，我们要根据要解决的问题，合理地选择使用其中哪种方法。

如果不知道哪种方法比较好，可以都尝试一遍，选择可视化效果更好的一个。

在本教程中，我们主要使用`catplot()`函数进行绘图，如前所述，该函数是基于其他许多函数基础上一个更高层次的调用渠道。

因此如果有针对其中任何一种方法的疑问，都可以在对应的方法的详细介绍中找到解释。

+++ {"slideshow": {"slide_type": "slide"}, "id": "C4C242381FD84125A7022ECB6C167711", "mdEditEnable": false, "jupyter": {}, "tags": []}

首先，我们需要导入需要的库`seaborn`和`matplotlib.pyplot`

```{code-cell} ipython3
---
id: 97B9F6ED91804703895FE9990E77DDA6
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
import seaborn as sns
import matplotlib.pyplot as plt
sns.set(style="ticks", color_codes=True)
```

### 分类散点图

+++ {"slideshow": {"slide_type": "slide"}, "id": "671F1A61FB8045898265A663216586A6", "mdEditEnable": false, "jupyter": {}, "tags": []}

`catplot()`中的默认绘图方法是`scatterplot`，在`catplot()`中。如果我们只有一个类别，那么散点图绘制的时候，许多数据点会重叠（overlap）在一起，数据区分度和美观性都不强。




```{code-cell} ipython3
---
id: AFA0F2C36DB04B508810762F8ABBF262
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
tips = sns.load_dataset('tips')
sns.relplot(x="day", y="total_bill", data=tips);
```

+++ {"id": "5F6CB4E30BF8486D8DCC2E3E7C6EF6CE", "jupyter": {}, "tags": [], "slideshow": {"slide_type": "slide"}, "mdEditEnable": false}

为了解决这一问题，实际上有两类绘制散点图的方法。


方法一： 我们可以考虑采用`stripplot()`，该方法通过给每一个数据点一个在`x`轴上的小扰动，使得数据点不会过分重叠。`stripplot()`是`catplot()`的默认参数。

```{code-cell} ipython3
---
id: 9C8C01854368455E84D3D93A74F77BD0
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="day", y="total_bill", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "8ACAD318A12C4B7F8903A836B90DFD27", "mdEditEnable": false, "jupyter": {}, "tags": []}

我们可以吧`jitter`参数关掉，观察一下效果。

```{code-cell} ipython3
---
id: 3F6B05CBC13943A9A85DC2DF09C80B4A
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="day", y="total_bill", jitter=0.3, data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "45B99E1D3957411A8B1EA5351476F846", "mdEditEnable": false, "jupyter": {}, "tags": []}

方法二： 使用`swarmplot()`，该方法通过特定算法将数据点在横轴上分隔开，进一步提高区分度，防止重叠。该方法对于小数据集尤其适用，调用该方法只需要在`catplot()`中指定参数`kind="swarm"`即可。

```{code-cell} ipython3
---
id: C4A76EF3EC0C458D82BE4C443802233A
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="day", y="total_bill", kind="swarm", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "9D0306F95B1C410F8459B52277F21291", "mdEditEnable": false, "jupyter": {}, "tags": []}

类似于`relplot()`,`catplot()`也可以通过添加颜色进一步增加绘图的维度，对应的参数为`hue`。需要注意的是，`catplot()`暂时不支持`sytle`和`size`参数。

```{code-cell} ipython3
---
id: 35632544F748491B8F7BC961B0124358
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="time", y="total_bill",kind="swarm", data=tips);
```

+++ {"id": "BE447184A431425885F571A55C55534F", "jupyter": {}, "tags": [], "slideshow": {"slide_type": "slide"}, "mdEditEnable": false}

不像数值型的数据，有的时候，我们对于离散型的类别数据很难得到一个排序的标准。当然，seaborn会尽可能地按照合理的方法给他们排序，如果需要的话也可以人为指定排序。

+++ {"id": "80F1AD0BD1CA4C3A8455EDAA1F9C3787", "jupyter": {}, "tags": [], "slideshow": {"slide_type": "slide"}, "mdEditEnable": false}

当我们想要指定绘制顺序的时候，可以使用`order`参数。

```{code-cell} ipython3
---
id: 084BCC20E52E47DE8C246BF3D7615B5F
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="smoker", y="tip", order=["Yes", "No"], data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "C246BFD2CEA24F03ACDAF45C0CDBA3E2", "mdEditEnable": false, "jupyter": {}, "tags": []}

有的时候，我们想要把散点图横着画，尤其是在类别比较多的时候，这时我们可以对调`x`和`y`参数，达到该效果。

```{code-cell} ipython3
---
id: 28C9E7AAAF774ACB8F6B3AE9EF3DBF8B
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="day", y="total_bill", hue="time", kind="swarm", data=tips);
```

+++ {"id": "3A8FC77707D343178163890CF78CF83D", "jupyter": {}, "tags": [], "slideshow": {"slide_type": "slide"}, "mdEditEnable": false}

**课堂练习：**

使用上面的方法，对tips数据集进行分析，绘制一个吸烟和吃饭时间（午饭or晚饭）与tip的关系图。你可以自定`x`,`y`轴和染色方法。

```{code-cell} ipython3
---
id: 26C23CFA6A6F477083927E92AA6312B9
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
# your code here
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "13F01AC01F2A4C6C83E8F9F11D4E2C86", "mdEditEnable": false, "jupyter": {}, "tags": []}




### 分类分布统计图

+++ {"slideshow": {"slide_type": "slide"}, "id": "EAA71122BB1443D59AE87635729263C2", "mdEditEnable": false, "jupyter": {}, "tags": []}

如前所述，类别形式的散点图受限于数据集的大小，当数据量很大时，即使是使用`swarmplot`或者`stripplot`也无法使数据点分开。此时，我们考虑使用基于数据分布的绘图方法，而不再采用散点图。

+++ {"slideshow": {"slide_type": "slide"}, "id": "34D5F174F79741EB89B5066568CC37B0", "mdEditEnable": false, "jupyter": {}, "tags": []}

### Boxplots

+++ {"id": "5B0D8F963D6F4A5DA766B8B70C0DD918", "jupyter": {}, "tags": [], "slideshow": {"slide_type": "slide"}, "mdEditEnable": false}



![Image Name](https://cdn.kesci.com/upload/image/q7dvvvog7u.jpg?imageView2/0/w/960/h/960)

箱形图（Box-plot）又称为盒须图、盒式图或箱线图，是一种用作显示一组数据分散情况资料的统计图。因形状如箱子而得名。在各种领域也经常被使用，常见于品质管理。

箱线图似乎是原始的，但它们具有占用较少空间的优势，这在比较许多组或数据集之间的分布时非常有用。


箱线图是一种基于五位数摘要（“最小”，第一四分位数（Q1），中位数，第三四分位数（Q3）和“最大”）显示数据分布的标准化方法。

- **中位数（Q2 / 50th百分位数）**：数据集的中间值；
- **第一个四分位数（Q1 / 25百分位数）**：最小数（不是“最小值”）和数据集的中位数之间的中间数；
- **第三四分位数（Q3 / 75th Percentile）**：数据集的中位数和最大值之间的中间值（不是“最大值”）；
- **四分位间距（IQR）**：第25至第75个百分点的距离；
- **离群值**
- **“最大”**：Q3 + 1.5 * IQR
- **“最低”**：Q1 -1.5 * IQR

+++ {"slideshow": {"slide_type": "slide"}, "id": "5740ECDAADFA41A68A0D28655E07519E", "mdEditEnable": false, "jupyter": {}, "tags": []}

基于分布的绘图方法中最简单的就是箱线图了，关于箱线图的理论已经在之前的讲义中进行了介绍，这里不再展开。箱线图的调用方法也很简单，直接`kind = "box"`就行。

```{code-cell} ipython3
---
id: DE36D68D4EBC4EA59D7702381BAECA4B
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="day", y="total_bill", kind="box", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "C96967D1046142CE9798951BBFFB2908", "mdEditEnable": false, "jupyter": {}, "tags": []}

当然了，我们还可以加入`hue`参数，增加数据的绘图维度。

```{code-cell} ipython3
---
id: D669830D82B043DCACBC9352917BC100
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="day", y="total_bill", hue="smoker", kind="box", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "F4FE00180EFA4BB8857E8F0A140B652C", "mdEditEnable": false, "jupyter": {}, "tags": []}

有一个和箱线图很像的图，叫`boxenplot()`，它会绘制一个跟箱线图很像的图片，但是展示了更多箱线图无法展示的信息，尤其适用于数据集比较大的情况。

```{code-cell} ipython3
---
id: FFB2A29ABEA14C7885E8A4E0FFE8CF4E
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
diamonds = sns.load_dataset("diamonds")

# diamonds = pd.read_csv('/home/kesci/input/Seaborn_Demo6897/diamonds.csv')

diamonds.head()
```

```{code-cell} ipython3
---
id: 3C9DA28FCC4A440983A9D538DB0A5C6A
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
#diamonds = sns.load_dataset("diamonds")
sns.catplot(x="color", y="price", kind="boxen",
            data=diamonds.sort_values("color"));
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "EE9EB6936B884098A2D44A826AA79908", "mdEditEnable": false, "jupyter": {}, "tags": []}

### Violinplots

+++ {"slideshow": {"slide_type": "slide"}, "id": "4FDAD2940A7C450D8EF959D01206560E", "mdEditEnable": false, "jupyter": {}, "tags": []}

接下来我们看小提琴图`violinplot()`，它结合了箱线图[核密度估计](https://mathisonian.github.io/kde/)的思想



```{code-cell} ipython3
---
id: D830195B51404D2EA63B349D56059BB7
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="total_bill", y="day", hue="time",
            kind="violin", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "4E7B00E2AD40473EAE42446BC80FDEDB", "mdEditEnable": false, "jupyter": {}, "tags": []}

该方法用到了kernel density estimate （KDE）,进而提供了更为丰富的数据分布信息。另一方面，由于KDE的引入，该方法也有更多的参数可以修改，例如`bw.`和`cut`

```{code-cell} ipython3
---
id: 327E744FF7794F6EB77627E9C0580EA8
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="total_bill", y="day", hue="time",
            kind="violin", bw=0.5, cut=0,
            data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "707CAC1FDB734E099DAB51B2E15B30E8", "mdEditEnable": false, "jupyter": {}, "tags": []}

此外，如果数据的`hue`参数只有两个类别，一种非常高效的方法是给定`split=True`,仅绘制具有对称性的图像的一半。

```{code-cell} ipython3
---
id: 9BE1D9EA23B1409B870DF4545108E85A
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="day", y="total_bill", hue="sex",
            kind="violin", split=True, data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "126F1D10434B48C893A1857F48BB3BC6", "mdEditEnable": false, "jupyter": {}, "tags": []}

当然了，小提琴图的内部绘制也可以修改，如果我们想要展示原始数据点而不是分位数等统计数据，我们可以指定`inner="stick"`,那么所有的原始数据点会被绘制在图中。

```{code-cell} ipython3
---
id: 5DCC6AE537D94F1C89DA77A92022AAE3
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
sns.catplot(x="day", y="total_bill", hue="sex",
            kind="violin", inner="stick", split=True,
            palette="Set1", data=tips);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "3370BF1CBAA549BE80B4D23A6C2ADC69", "mdEditEnable": false, "jupyter": {}, "tags": []}

我们还可以把`swarmplot()`或者`striplot()`放置在`boxplot`或者`violinplot`中，从而实现总体与局部的整体展示。

```{code-cell} ipython3
---
id: 2E09DD5F03A54DF38F7E1A78674B187C
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
g = sns.catplot(x="time", y="total_bill", kind="violin", inner=None, data=tips)
sns.swarmplot(x="time", y="total_bill", color="k", size=3, data=tips, ax=g.ax);
```

```{code-cell} ipython3
---
id: 51CEDEF5DBA544DF8D9ED532BE91136C
jupyter: {}
slideshow:
  slide_type: slide
tags: []
---
g = sns.catplot(x="day", y="total_bill", kind="box",data=tips)
sns.swarmplot(x="day", y="total_bill", color="k", size=3, data=tips, ax=g.ax);
```

+++ {"slideshow": {"slide_type": "slide"}, "id": "DD9DF13283FD44C08D3817929BFF1F91", "mdEditEnable": false, "jupyter": {}, "tags": []}



