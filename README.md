###百度地图API GPS转百度批量转换

核心代码

```js
var total = 0; //总记录数
var groupCount = 0; //每次转十条
if (points.length % 10 > 0) {
	groupCount = (points.length / 10) + 1;
}
else {
	groupCount = (points.length / 10);
}

for(var i=0;i<groupCount;i++){ //外层循环，有多少组十条
	var pos = new Array();
	for(var j=0;j<10;j++){ //内层循环，每组十条
		if(total<points.length){ //不超过总记录数结束
			var point = new BMap.Point(points[(i * 10) + j].lng,points[(i * 10) + j].lat);
			pos.push(point);
		}
		total++;
	}
	
	var convertor = new BMap.Convertor();
	convertor.translate(pos, 1, 5, function(data){
		if(data.status === 0) {
			for (var i = 0; i < data.points.length; i++) {
				bm.addOverlay(new BMap.Marker(data.points[i]));
				bm.setCenter(data.points[i]);
			}
		  }
	});
	
}
```

演示地址：http://itmyhome.com/baidu_map_batch_conversion