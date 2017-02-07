#a-template.js

Simple Template Engine
used for [gulp-generator](https://github.com/steelydylan/gulp-generator)


##example

```html
<!DOCTYPE html>
<html lang="ja">
<head>
	<meta charset="UTF-8">
	<title>list sample</title>
</head>
<body>
	<script id="list_template" type="text/template">
	<ul>
		<li><input type="text" data-bind="newItem"><button data-action="addItem()">追加</button></li>
		<!-- BEGIN list:loop -->
		<li>{name}[addMr]<button data-action="removeItem({i})">削除</button></li>
		<!-- END list:loop -->
	</ul>
	</script>
	<script src="https://code.jquery.com/jquery-1.11.3.min.js"></script>
	<script src="../aTemplate.js"></script>
	<script>
	var list = new aTemplate.View({
		templates:["list_template"],
		data:{
			list:[
				{name:"tomomi"},
				{name:"daigo"},
				{name:"taro"},
				{name:"koike"}
			]
		},
		method:{
			removeItem:function(i){
				this.data.list.splice(i,1);
				this.update();
			},
			addItem:function(){
				console.log(this.data.newItem);
				this.data.list.push({name:this.data.newItem});
				this.update();
			}
		},
		convert:{
			addMr:function($txt){
				return "Mr."+$txt;
			}
		}
	});
	list.update();
	</script>
</body>
</html>
```
