# :eyeglasses:表单与v-model #

<b id="t"></b>

:one:[基本用法](#a1)

:two:[绑定值](#a2)

:three:[修饰符](#a3)

<p id="a1"></p>

### :cool:基本用法 ###

:arrow_double_up:[返回目录](#t)

Vue提供了v-model指令，用于在表单类元素上双向绑定数据，可以根据实时更新数据，如下面的例子：

```vue
<body>
	<div id="box">
		<input type="text" placeholder="输入内容..." v-model="message">	
		<p>正在输入：{{message}}</p>
	</div>
			
	<script>
				
	var app = new Vue({
		el : '#box',
		data : {
			message : ''
		}
	});
	</script>
</body>
```

像这样会实时刷新数据。还能将数据绑定到message上。其余输入表单也是一样的，连密码框也具有同样的效果。对于v-model还有语法糖@input来表示，也可以使用方法进行绑定：

```vue
<body>
	<div id="box">
		<input type="text" placeholder="输入内容..."  @input="handleInput">	
		<p>正在输入：{{message}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			message : ''
		},
		methods : {
			handleInput : function(e){
				this.message = e.target.value.toLocaleUpperCase();;
			}
		}
	});
	</script>
</body>
```

如上就是实时大写转换。

**单选按钮**


单选按钮在单独使用时，不需要v-model，直接使用v-bind绑定一个布尔值，为真代表选中，为否则是不选。如下：

```vue
<body>
	<div id="box">
		<input type="radio" v-model="picked" value="YES">	
		<label>YES</label><br>
		<input type="radio" v-model="picked" value="NO">	
		<label>NO</label><br>		
		<h3>你选择了{{picked}}</h3>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			picked : 'NO'
		}
	});
	</script>
</body>
```

**复选框**

复选框也分单独使用和组合使用，不过用法稍微与单选不同，复选框单独使用时需要v-model来绑定一个布尔值，如：

```vue
<body>
	<div id="box">
		<input type="checkbox" v-model="Select" value="A">	
		<label>Select A</label><br>
		<input type="checkbox" v-model="Select" value="B">	
		<label>Select B</label><br>		
		<h3>你选择了{{Select}}</h3>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			Select : []
		}
	});
	</script>
</body>
```

**选择列表**

选择列表也分单选与多选，单选如下：

```vue
<body>
	<div id="box">
			<select v-model="Select">
				<option value="A">A</option>
				<option>B</option>
				<option>C</option>
				<option>D</option>
			</select>
			<p>你的选项是:{{Select}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			Select : ''
		}
	});
	</script>
</body>
```

单选为单值，多选就为数组。如下当为数组时，即为多选：

```vue
<body>
	<div id="box">
			<select v-model="Select" multiple>
				<option value="A">A</option>
				<option>B</option>
				<option>C</option>
				<option>D</option>
			</select>
			<p>你的选项是:{{Select}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			Select : []
		}
	});
	</script>
</body>
```

这里值得注意的是在select标签上要加上multiple属性才能让鼠标多选。

在运用中option一般都是用v-for导出来的，value与text都是一样的导出，如下：

```vue
<body>
	<div id="box">
			<select v-model="Select" multiple>
				<option v-for="option in options" :value="option.value">{{option.text}}</option>
			</select>
			<p>你的选项是:{{Select}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			Select : [],
			options : [
				{text : '选项A',value : 'A'},
				{text : '选项B',value : 'B'},
				{text : '选项C',value : 'C'},
				{text : '选项D',value : 'D'}
			]
		}
	});
	</script>
</body>
```

但是这样表单控件不太美观，可以使用组件来优化，将在后面介绍组件的使用。

<p id="a2"></p>

### :cool:绑定值 ###

:arrow_double_up:[返回目录](#t)

前面介绍的单选，复选框在单选模式下，只能绑定一个静态字符串和一个布尔值，如果需要动态数据值，则需要绑定一个新数据：

```vue
<body>
	<div id="box">
		<input type="radio" v-model="picked" :value="value"><label>是否选择</label>	
		<p>{{picked}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			picked : false,
			value : '已选中'
		}
	});
	</script>
</body>
```

当点击时，picked的值会与value值一样。复选框也是一样的

```vue
<body>
	<div id="box">
		<input type="checkbox" v-model="picked" :true-value="value1" :false-value="value2"><label>是否选择</label>	
		<p>{{picked}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			picked : false,
			value1 : '已选中',
			value2 : '未选中'
		}
	});
	</script>
</body>
```

<p id="a3"></p>

### :cool:修饰符 ###

:arrow_double_up:[返回目录](#t)

有事件的修饰符类似，v-model也有修饰符，用于控制数据同步的时机。

.lazy ：在输入框中，v-model会默认是在input事件同步输入框的数据，使用该修饰符会转变为在change事件中同步，如下：

```vue
<body>
	<div id="box">
		<input type="text" v-model.lazy="value" ><label>是否选择</label>	
		<p>{{value}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			value : ''
		}
	});
	</script>
</body>
```

如上会在失去焦点后触发事件。更新视图。

.number ： 使用修饰符.number可以将输入转换为Number类型，否者虽然你输入的是数组，但它的类型是String，比如在数字输入框时会比较有用，示例代码如下：

```vue
<body>
	<div id="box">
		<input type="text" v-model.number="value" ><label>是否选择</label>	
		<p>{{value+1}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			value : 0
		}
	});
	</script>
</body>
```

如上，像这样才能触发number+1，没有这个修饰符则是字符串+1类型值。


.trim ：修饰符.trim可以自动过滤输入的首尾空格，示例代码如下：

```vue
<body>
	<div id="box">
		<input type="text" v-model.trim="value" ><label>是否选择</label>	
		<p>{{value}}</p>
	</div>
	<script>
	var app = new Vue({
		el : '#box',
		data : {
			value : ''
		}
	});
	</script>
</body>
```







