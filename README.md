# layui-learning
学习layui的一些收获

## 背景说明
配合mentor做后台管理系统，学习layui。<br>
在这里记录下学习的路径和遇到的坑。

## 学习材料 
[B站讲解视频,主讲声音超级温柔](https://www.bilibili.com/video/BV1PK411g7T7?p=2)<br>
[layui官方文档](https://www.bilibili.com/video/BV1PK411g7T7?p=2)

## 对layui的理解
首先这是方便后端快速上手的框架，可以理解为后端已经扎好了稻草人，layui帮忙做下套皮装饰和数据捕获。<br><br>
基本的使用逻辑：layui已经写好了模块，前端要做的事情是在html页面，导入layui的css和js文件，使用layui.use（）进行模块调用即可。<br>
ps：翻了下官网说的AMD时代，AMD是"Asynchronous Module Definition"的缩写，意思就是"异步模块定义"，但我暂时没有那么深的体悟，先搁这吧……<br><br>
在css上和bootstrap用法比较像，因此除了理解响应式的栅格布局之外，学习重点应该放在form和table上（毕竟是处理数据的嘛）。<br>
ps：这里耗费了比较多的时间在看css，不是很有必要，可以用到再慢慢调。

## 模块导入注意事项

先建个项目，css/js/img文件夹搞起，把layui下载后解压直接拖进来，单独成一个文件夹。
### 导入css和js
```<link rel="stylesheet" href="./layui/css/layui.css">
<script src="./layui/layui.js"></script>
```
ps:script写在body腹部当然是比较好的，这里是演示方便起见。在页面元素部分其实都用不着加载js文件来着。

### 页面元素
这里说下栅格布局和按钮（真的是因为东西太碎了，好想模仿大佬说一句，用的时候翻文档吧……）

#### 栅格布局
先给大容器，再给行和列。一行十二栏，栏栏往下分。
示例demo：
```
<div class="layui-container">   //先给大容器
  常规布局（以中型屏幕桌面为例）：
  <div class="layui-row"> //再给行
    <div class="layui-col-md9"> //再给列
      你的内容 9/12
    </div>
    <div class="layui-col-md3"> //和前面的盒子一起分12行
      你的内容 3/12
    </div>
  </div>
```

#### 元素变按钮
加上`.layui-btn`就是可以完成了。
```
<a href="www.https://www.layui.com/" class="layui-btn">跳转官网的按钮</a>
<div class="layui-btn">没啥用但是就搁在这表示div也可以变身的按钮</div>
```

### form表单
#### 依赖form组件，记得载入。
```
<script>
layui.use('form', function(){
  var form = layui.form;})
</script>  
```
#### 在一个容器中设定class="layui-form"来标识一个表单元素块
```
<form class="layui-form" action="">
</form>
```
#### 往里面搁行区块（注意需要定义.layui-form）
```
<form class="layui-form" action="">
	<div>
		<label class="layui-form-label">标签区域</label>
		<div class="layui-input-block">
			原始表单元素区域
		</div>
	</div>
</form>
```
#### 写写原始表单元素区域
demo：
```
<form class="layui-form" action="">
	<div>
		<label class="layui-form-label">标签区域</label>
		<div class="layui-input-block">
			<input type="text" name="title" class="layui-input"> //搁个文本框
		</div>
	</div>
</form>
```
#### 一些常用的框框
##### 下拉选择框
```
<select name="city" lay-verify="">
	<option value="010">北京</option>
	<option value="013">上海</option>
	<option value="024">广州</option>
</select>
```
有两个比较有特色的东西，一个是分组，一个是搜索匹配。
①分组（添加一个空option，添加optgroup)：
```
<select name="city" lay-verify="">
	<option value="">请选择</option>
	<optgroup label="您将从哪出发？">
		<option value="010">北京</option>
		<option value="013">上海</option>
		<option value="024">广州</option>
	</optgroup>
	<optgroup label="您将到哪儿去？">
		<option value="011">秦皇岛</option>
		<option value="018">苏州</option>
		<option value="056">深圳</option>
	</optgroup>
</select>
```
②搜索（添加一个lay-search就好）
```
<select name="city" lay-verify="" lay-search>
	<option value="010">北京</option>
	<option value="013">上海</option>
	<option value="024">广州</option>
</select>
```
##### 复选框
注意设置复选框前面的文本，是在title属性里改。
`<input type="checkbox" name="hobby" title="写代码">`

##### 组装行内表单
把几个框框搁一排。
思路：外层form-item(把一个行变成容器)，内层inline（横排）
并列【标签1】和【标签2】的栗子：
```
<div class="layui-form-item">
	<div class="layui-inline">
		<label class="layui-form-label">标签1</label>
		<div class="layui-input-inline">
			标签1-行内小块1
		</div>
		<div class="layui-input-inline">
			标签1-行内小块2
		</div>
		
	<div class="layui-inline">
		<label class="layui-form-label">标签2</label>
		<div class="layui-input-inline">
			标签2-行内小块1
		</div>
		<div class="layui-input-inline">
			标签1-行内小块2
		</div>
			
	</div>
</div>
```
这里还有些装饰物，比如lay-ignore（原始效果）,layui-form-pane（方框风格，注意这个要加到form标签那），慢慢探索……

今天就写到这吧，明天写下组件。

