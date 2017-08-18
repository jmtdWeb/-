<!doctype html>
<html lang="zh-CN">
<head>
<meta charset="utf-8">
<title>测试验证</title>
<meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, telephone=no" name="viewport">
<meta content="telephone=no" name="format-detection" />
<meta content="yes" name="apple-mobile-web-app-capable" />
</head>

<body>
<div id="box">
	 <div class="time" data-time="1599972000" style="color:red"></div>  
	 <div class="time" data-time="1599972600" style="color:red"></div>
	 <div class="time" data-time="1599973200" style="color:red"></div>
</div>
<button id="but">加载新数据</button>
<script>
function timeNew(id){
	this.id = id;
	this.ti = null;
	this.className = document.getElementsByClassName(this.id);
	this.li = this.className.length;
	if(this.li >= 1){
		this.list();
	}
}
timeNew.prototype = {
	list:function(){
		for(var i=0; i<this.li; i++){
			this.fc(this.className[i]);
		}
	},
	fc:function(classNameFun){
		var val  = classNameFun.getAttribute('data-time');
		var html = this.time(val - Date.parse(new Date())/1000);
		classNameFun.innerHTML = html;
		if (this.ti) {
			clearTimeout(this.ti);
		}
		this.ti = setTimeout(function(self) {
			return function() {
				self.list();
			}
		}(this), 1000);
	},
	time:function(d){
		if(d>0){
			var t = parseInt(d/60/60/24);
			var s = parseInt((d - t*24*60*60)/60/60);
			var f = parseInt((d - t*24*60*60 - s*60*60)/60);
			var m = d - t*24*60*60 - s*60*60 - f*60;
			return '剩余'+t+'天'+s+'小时'+f+'分'+m+'秒';
		}else{
			return '时间已经到了！';
		}
	}
}
var a = new timeNew('time');
/*
 * 加载新数据
 */
var sj = 1599994200;
document.getElementById('but').onclick = function(){
	var name = document.getElementById('box');
	var html = name.innerHTML;
	name.innerHTML = html + '<div class="time" data-time="'+sj+'" style="color:red">努力加载中</div>';
	sj += 600;
	a.li++;
}
</script>  
</body>
</html>
