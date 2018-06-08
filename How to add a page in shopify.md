作者：吴业飞
时间：2018.06.08


---

这个教程将说明如何在一个shopify的theme中新建一个页面并正确的指向这个页面。

## 实际工作流程

### 1.Add a section


![image.png | center | 364x206](https://cdn.yuque.com/yuque/0/2018/png/126695/1528441413911-85118287-d4d7-413f-91d6-f7592dffe8f6.png "")


我们新增一个名为my-first-section的section,这个section里编写的HTML代码就是你新增的页面的HTML
> Tips: shopify自带的在线编辑器比较难用，建议在自己习惯的编辑器里完成编码后粘贴过来。
> 准确的说这个不是HTML文件，而是liquid模板引擎，关于liquid模板语法的介绍可以看[https://github.com/Shopify/liquid](https://github.com/Shopify/liquid)
> Note: schema请写在section中

### 2.Add a Templates



![image.png | left | 819x649](https://cdn.yuque.com/yuque/0/2018/png/126695/1528442637531-e9630936-9348-485a-83ca-7e95bd221891.png "")


这里我们新建一个名为my-first-page的Template


![image.png | left | 825x105](https://cdn.yuque.com/yuque/0/2018/png/126695/1528443337341-8f468b8b-3d55-4763-9d42-7fbf12b03229.png "")


可以看到my-first-page并不是一个空白的文件，这里自动生成的代码我们点开Template下的page.liquid就明白了



![image.png | left | 827x122](https://cdn.yuque.com/yuque/0/2018/png/126695/1528443949171-6114f24a-89cc-4211-a33d-4b7010771f13.png "")


可以看到因为我们在新建名为my-first-page的Template时选择了for page，所以my-first-page继承了page.liquid的内容。那么问题来了，我们现在是在新建页面，我们就想从零开始不想继承，能不能不选择for page呢？答案是否定的，在后面会说到原因。
我们现在回归正常工作流程，我们新建了section,新建了template，现在我们在template中引用我们的section,通过
{% section 'my-first-section' %}



![image.png | left | 827x115](https://cdn.yuque.com/yuque/0/2018/png/126695/1528444789587-74a29264-c6da-4d9f-94e7-c461d5b46f17.png "")


可以看到，我们并没有在我们的template中编写HTML，我们选择将所有的HTML放到section中，只在template中引入section,理由是我们可能需要编写schema,而schema必须编写在对应的section中才能生效（全局schema除外）。
至此我们的HTML部分编码完成，我们再将我们编写好的SCSS粘贴到Assets下的__theme.scss.liquid__
> 官方指南中说明了我们可以在section中用{% stylesheet %}
{% endstylesheet %}
包裹该section所需的css(scss),这里建议将SCSS放到总的样式文件__theme.scss.liquid__的理由是笔者在实践中发现写在section中的样式貌似不能在刷新页面后立刻生效，总感觉有延迟要多次刷新，但是写在__theme.scss.liquid__中可以在刷新后立即生效，这个问题有待验证原因。在此提出以便读者在实践中如果发现样式未生效不妨将样式放到theme.scss.liquid文件中看看效果以便排查错误。

### 3.Add page

下面的流程不涉及编码，单纯地在前台添加我们写好的页面。



![01.png | left | 827x394](https://cdn.yuque.com/yuque/0/2018/png/126695/1528451411695-ca1f7513-56a5-4012-a86b-db874a20df9e.png "")




![02.png | left | 827x441](https://cdn.yuque.com/yuque/0/2018/png/126695/1528451483508-04a5788b-1e01-4636-8fd4-6e13891abacb.png "")


### 4.访问页面

经过上述步骤我们已经在系统里添加了页面，本小节将说明怎么访问这些页面。
#### object handles
Handles是用来访问对象属性的，具体介绍参考[https://help.shopify.com/themes/liquid/basics/handle](https://help.shopify.com/themes/liquid/basics/handle)
这里我们直接说明访问页面的url
如果我们在Add page时选择的Template suffix是page.my-first-page，那么url为/pages/my-first-page。
shopify的命名规范是全部小写“-”分割，所以为了方便url的书写建议__不要__使用驼峰命名法。




---

版权声明：自由转载-非商用-非衍生-保持署名


