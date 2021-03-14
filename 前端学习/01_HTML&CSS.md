# HTML&CSS

## 一：HTML语法

```html
<p>...</p>              //段落文本
<div>...</div>          //块状分组
<span>...</span>        //行内分组
<textarea>...</textarea>    //多行文本输入

<a>...</a>              //链接标签
<hr>...</hr>            //水平线标签

<strong>...</strong>	//强调变粗
<b>...</b>              //仅仅变粗

<em>...</em>            //强调倾斜
<i>...</i>              //仅仅倾斜

<del>...</del>          //删除元素
<ins>...</ins>          //下划线元素
<s>...</s>              //错误的内容
<u>...</u>              //拼写错误的单词或者汉语中的专有名词
<mark>...</mark>        //标记元素
<sup>...</sup>          //上标
<sub>...</sub>          //下标
<small>...</small>      //变小

<ul>
    <li>...</li>        //无序列表
    <li>...</li>
</ul>

<ol>
    <li>...</li>        //有序列表
    <li>...</li>
</ol>

<dl>                    //定义列表
    <dt></dt>           //定义项目内容
    <dd></dd>           //定义描述部分内容
</dl>

<form>...</form>        //表单，属性method:允许使用哪一种方法向服务器提交表单get/post，通常使用post
                        //属性：autocomplete，是否记忆已经输入过的内容
<input>                 //输入,属性radio:单选框；checkbox:复选框--属性中可以有选择时间；search：搜索框；entype：上传文件必要属性
                        //list属性与datalist关联使用
<output>...</output>    //输出
<label>...</label>      //隐式关联，绑定单行文本框
<fieldset>...
    <legend>...</legend>  //fieldset说明

</fieldset>  //元素分组

//下拉选项框
<select>
    <option>...</option>
</select>
<optgroup></optgroup>   //对option进行分组

<map>...</map>          //图片映射
<area>...</area>        //映射地址

<picture>...</picture>  //图片
<figure>...</figure>    //插图

<video></video>         //嵌入视频
<audio></audio>         //嵌入音频
<track>                 //加载字幕
<iframe></iframe>       //嵌入另一个网页
```

表格：

```html
<caption>表格标题</caption>
<table>
    <tr>
        //tr定义行
        <th>表头</th>
        <td>数据单元格</td>
        //th\td属性：colspan横跨列数；rowspan纵跨行数
    </tr>
</table>

<thead>\<tbody>\<tfoot>    //对表格进行细分
```



## 二：常用的CSS属性

### 1、与HTML关联方法：

- 内联样式：style指定
- 内部样式表：头部通过style样式
- 外部样式表：（相同样式可以用于多个文件）通过link与HTML进行关联

==注==：三种样式优先级依次降低

### 2、选择器

- 通用选择器
- 元素选择器

- 类选择器：.class（不唯一）
- id选择器：#id（唯一，可以用来定义单个元素）

### 3、复合选择器

- 交集选择器：元素选择器.类选择器|元素选择器#id选择器
- 并集选择器：选择器1,选择器2,选择器3...
- 后代选择器：选择器1 选择器2 选择器3...（中间加空格）
- 子元素选择器：选择器1 > 选择器2 （选择器1指定元素的所有选择器2指定的==直接==子元素）
- 相邻元素选择器：选择器1 + 选择器2（选择紧跟在选择器1指定元素后出现的选择器2指定的元素，而且这两个元素有共同的父元素）
- 通用兄弟选择器：选择器1 ~ 选择器2（==选择器2不用紧跟在选择器1之后==）

### 伪选择器

引入伪类和伪元素原因：为了格式化文档树以外的信息

伪类用于当已有元素处于的某个状态时，为其添加样式（==如无必要，勿增实体==，减少元素的实体说明）

伪元素用于创建一些不在文档树的元素，为其添加样式（==如无必要，勿增实体==）

- 伪元素选择器： ::first-line（仅对块级元素内的第一行内容有效） ::first-letter（选中文本框的第一个字符） ::before|::after（生成新的内容插入HTML中） ::selection（匹配用户选中的部分文本）
- 伪类选择器
  - 动态伪类：（根据条件改变匹配元素）:link|:visited|:hover|:active（先后区别）|:focus
  - UI伪类：:enabled|:disabled|:checked|:required|:optional|:default|:valid|:in-range|:out-of-range|:read-only|:read-write
  - 结构伪类：:root|:empty|:first-child|:last-child|:only-child|:only-of-type|:first-of-type|:last-of-type|:nth-child(n)|:nth-last-child(n)|
  - 其他：:target|:lang|:not|

### 属性选择器

- [class = " "]



```css
list-style-type    //设置列表的标志
list-style-image   //用图片设置列表标志

border-collapse    //可以用于设置表格边框线
padding            //调整单元格内边距
background         //背景属性
display:block      //将元素指定为块级元素
display:inline     //将元素指定为行内元素
display:inline-block    //行内块元素
```

### 4、float属性

float:用于元素浮动，进行多列布局，float元素会覆盖块级元素

### 5、自动创建一个新的BFC

- float属性的值不为none
- position属性的值不为static或relative
- overflow属性值不为visible
- display属性的值为flex，inline-flex，inline-block，table-cell或table-caption

### 6、布局

- 居中：水平居中（text-align）垂直居中（line-height）
- 双飞翼布局：（三列布局）先把中间布置好，再将左右两列移动到合适的位置（通过margin负值法进行移动左右两列）
- 圣杯布局：左列与容器的左边距重叠，右列与容器的右边距重叠，中间列充满容器的宽度（通过margin负值法进行移动左右两列）
- 瀑布流布局：
- 弹性盒布局：display:flex|display:inline-flex
  - 主轴：规定了弹性元素排布的顺序
  - 垂轴：决定了在发生换之后，第二行元素的添加方向