# :eyeglasses:v-bind及class与style绑定 #

<b id="t"></b>

:one:[绑定Class的几种方式](#a1)

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

```

```








