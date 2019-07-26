# :eyeglasses:v-bind及class与style绑定 #

<b id="t"></b>

:one:[绑定Class的几种方式](#a1)

:two:[绑定内联的样式](#a2)

<p id="a1"></p>

### :cool:绑定Class的几种方式 ###

:arrow_double_up:[返回目录](#t)

给v-bind:class设置一个对象，可以动态地切换class，比如：

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script src="https://unpkg.com/vue@2.1.6/dist/vue.min.js"></script>
	</head>
	<style>
		.active{
			color: brown;
		}
	</style>
	<body>
		<div id="app" >
			<p :class="{'active' : isActive }">Hello</p><br>
			<button @click='change'>点击变色</button>
		</div>
		<script>
			var app = new Vue({
				el : '#app',
				data : {
					isActive : false
				},
				methods : {
					change : function(){
						this.isActive = true;
					}
				}
			})
		</script>
	</body>
</html>
```

上面的示例中，类名active依赖数据isActive，当其为true时，div会拥有类名Active，为false时则没有，所以上面代码渲染后就是

`<p class="active">Hello</p>`

对象中也可以传入多个属性，来动态切换class，另外:class与普通class共存，例如：

```vue
	<style>
		.css1{
			color: blue;
		}
		.css2{
			color: brown;
		}
	</style>
	<body>
		<div id="app" >
			<p :class="{'css1' : isShow1, 'css2' : isShow2}">Hello</p><br>
			<button @click='change'>点击变色</button>
		</div>
		<script>
			var app = new Vue({
				el : '#app',
				data : {
					isShow1 : false,
					isShow2 : true
				},
				methods : {
					change : function(){
						this.isShow1 = true;
						this.isShow2 = false;
					}
				}
			})
		</script>
	</body
```

当某一个选项为真时，其类名就会被渲染，如果多个为真，那就渲染多个类。当:class过长时，可以使用计算属性，一般当条件多余2个时，都可以使用计算属性：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script src="https://unpkg.com/vue@2.1.6/dist/vue.min.js"></script>
	</head>
	<style>
		.css1{
			color: blue;
		}
		.css2{
			color: brown;
		}
	</style>
	<body>
		<div id="app" >
			<p :class="classes">Hello</p><br>
			<button @click='change'>点击变色</button>
		</div>
		<script>
			var app = new Vue({
				el : '#app',
				data : {
					isShow1 : false,
					isShow2 : true
				},
				computed :{
					classes : function(){
						return {
							css1 : this.isShow1,
							css2 : this.isShow2
						}
					}
				},
				methods : {
					change : function(){
						this.isShow1 = true;
						this.isShow2 = false;
					}
				}
			})
		</script>
	</body>
</html>
```


**数组用法**

当需要应用多个class时可以使用数组语法，给：class绑定一个数组，应用一个class列表：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script src="https://unpkg.com/vue@2.1.6/dist/vue.min.js"></script>
	</head>
	<style>
		.css1{
			color: blue;
		}
		.css2{
			color: brown;
		}
	</style>
	<body>
		<div id="app" >
			<p :class=[cssStyle1,cssStyle2]>Hello</p><br>
			<button @click='change'>点击变色</button>
		</div>
		<script>
			var app = new Vue({
				el : '#app',
				data : {
					cssStyle1 : 'css1',
					cssStyle2 : ''
				},
				methods : {
					change : function(){
						this.cssStyle1  = '';
						this.cssStyle2 = 'css2';
					}
				}
			})
		</script>
	</body>
</html>
```

当然也可以使用三元表达式来切换css：

```html
<div id="app" >
	<p :class="[isActive ?  cssStyle1 : '' , cssStyle2 ]">Hello</p><br>
	<button @click='change'>点击变色</button>
</div>
<script>
			var app = new Vue({
				el : '#app',
				data : {
					isActive  : true,
					cssStyle1 : 'css1',
					cssStyle2 : ''
				},
				methods : {
					change : function(){
						this.cssStyle1  = '';
						this.cssStyle2 = 'css2';
					}
				}
			})
</script>
```

也可以采用对象的写法：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script src="https://unpkg.com/vue@2.1.6/dist/vue.min.js"></script>
	</head>
	<style>
		.css1{
			color: blue;
		}
		.css2{
			color: brown;
		}
	</style>
	<body>
		<div id="app" >
			<p :class="[{'css1' : isShow1 },{'css2' : isShow2}]">Hello</p><br>
			<button @click='change'>点击变色</button>
		</div>
		<script>
			var app = new Vue({
				el : '#app',
				data : {
					isShow1 : true,
					isShow2 : false
				},
				methods : {
					change : function(){
						this.isShow1  = false;
						this.isShow2 = true;
					}
				}
			})
		</script>
	</body>
</html>
```

<p id="a2"></p>

### :cool:绑定内联的样式 ###

:arrow_double_up:[返回目录](#t)

使用v-bind:style(:style)可以给元素绑定内联样式。与class一样。有数组有对象写法：

```html
		<div id="app" >
			<p :style="{'color' : color,'fontSize':fontSize+'px'}">Hello</p><br>
			<button @click='change'>点击变色</button>
		</div>
		<script>
			var app = new Vue({
				el : '#app',
				data : {
					color : 'red',
					fontSize : 18
				},
				methods : {
					change : function(){
						this.color = 'blue';
						this.fontSize = 22;
					}
				}
			})
		</script>
```

也可以使用类封装：

```vue
		<div id="app" >
			<p :style="styles">Hello</p><br>
			<button @click='change'>点击变色</button>
		</div>
		<script>
			var app = new Vue({
				el : '#app',
				data : {
					styles : {
						color : 'red',
						fontSize : '18px'
					}
				},
				methods : {
					change : function(){
						this.styles.color = 'blue';
						this.styles.fontSize = '22px';
					}
				}
			})
		</script>
```
