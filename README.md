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

2021.09.17 更新-组件部分
## 常用组件介绍
这篇学习笔记主要记录弹出层（layer）、日期（laydate）、分页、数据表格的使用方法。
组件的使用思路是在html页面里给个盒子，然后通过js绑定盒子，把内容导进去。
和苔藓微景观制作思路比较像。微型景观制作好了，但没有在现场，需要搬过来，然后给个玻璃缸装上。

## layer
弹出层，是一个单独使用也非常高频的组件。注意独立使用，需要在layer.js之前需要先引入jquery，下面介绍的是模块化使用方法。

### 引入方法
引入layui的css与js文件后，在script中使用layui.use（）加载模块

#### layer（弹出层）
##### 基础参数
[万事不决问文档](https://www.layui.com/doc/modules/layer.html)
这里说下使用思路，type控制传入类型，title是弹出层的标题，content则是弹出层的内容。
大概类似于进蛋糕店，先和店员说要个什么类型的蛋糕，上面的贺卡要写啥，蛋糕应该是什么样。
ps:注意content里面给到的是数组
pps：layer.msg() //yyds!

#### laydate（日期）
[万事不决问文档](https://www.layui.com/doc/modules/laydate.html)
看介绍貌似是个古老的坑得到了新填，这个组件开启range后在chorme上的显示效果有点诡异（右栏留白），在edge上效果还挺好的。

#### page（分页）
[万事不决问文档](https://www.layui.com/doc/modules/laypage.html)
搞不懂为啥到绑定elem忽然就不要井号了……
count在最开始练习的时候写死，后期可以通过从后台获取数据进行重构。
curr一般是给1，从第1页开始查询。
注意要出现翻页的前后箭头，用`layout:['prev', 'page', 'next']`
ps:自己的js学的是真得一般般，数据渲染部分完全没沾到……要加油！

#### table（数据表格）
[万事不决问文档](https://www.layui.com/doc/modules/table.html)
小白前端看文档看到“一切都是那么熟悉”晕了哈哈哈，B站教学视频里面是新建一个json文件，然后把返回数据粘进去，再慢慢写html页面。

##### 渲染方法
表格渲染有三种方式，官方比较推荐的是方法渲染。
方法渲染是啥呢，接着用微缩景观那个比方吧，就是微缩景观全部用js制作，全部做完了再搬到空的大玻璃缸里，这样手艺人只要集中精力在js上就可以了。
自动渲染则是先进到缸子里，然后边搭边做搭配调整。
转换静态表格就是前人辛辛苦苦在缸子里搭了些微缩景观，但没用到layui，于是需要给它们粘上定位符，然后让layui自动粘上去。

##### 开启分页
开启分页的方法就是往render里丢个page:true（记得逗号不要忘了）。

##### 开启表头
官方说要驾驭不了layui table，注意力搁这准没错。
给个栗子：
```
//方法渲染：
table.render({
  cols:  [[ //标题栏
    {checkbox: true}
    ,{field: 'id', title: 'ID', width: 80}
    ,{field: 'username', title: '用户名', width: 120}
  ]]
});
```


##### 绑定工具条模板
直接上官方栗子吧：
```
<script type="text/html" id="barDemo">
  <a class="layui-btn layui-btn-xs" lay-event="detail">查看</a>
  <a class="layui-btn layui-btn-xs" lay-event="edit">编辑</a>
  <a class="layui-btn layui-btn-danger layui-btn-xs" lay-event="del">删除</a>
  
  <!-- 这里同样支持 laytpl 语法，如： -->
  {{#  if(d.auth > 2){ }}
    <a class="layui-btn layui-btn-xs" lay-event="check">审核</a>
  {{#  } }}
</script> //这段laytpl语法没太懂是什么东西....
 
注意：属性 lay-event="" 是模板的关键所在，值可随意定义。
```
绑定监听：
```
//工具条事件
table.on('tool(test)', function(obj){ //注：tool 是工具条事件名，test 是 table 原始容器的属性 lay-filter="对应的值"
  var data = obj.data; //获得当前行数据
  var layEvent = obj.event; //获得 lay-event 对应的值（也可以是表头的 event 参数对应的值）
  var tr = obj.tr; //获得当前行 tr 的 DOM 对象（如果有的话）
 
  if(layEvent === 'detail'){ //查看
    //do somehing
  } else if(layEvent === 'del'){ //删除
    layer.confirm('真的删除行么', function(index){
      obj.del(); //删除对应行（tr）的DOM结构，并更新缓存
      layer.close(index);
      //向服务端发送删除指令
    });
  } else if(layEvent === 'edit'){ //编辑
    //do something
    
    //同步更新缓存对应的值
    obj.update({
      username: '123'
      ,title: 'xxx'
    });
  } else if(layEvent === 'LAYTABLE_TIPS'){
    layer.alert('Hi，头部工具栏扩展的右侧图标。');
  }
});
```
注意layer-filter是精髓哈，命名一定要和下面的tool(事件名)对应起来。
这个部分掌握得很一般，下个周做一下demo继续完善吧~




