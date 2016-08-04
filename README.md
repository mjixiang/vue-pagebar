# vue-pagebar
A paging component for Vue.js
基于Vue.js的分页组件

##示例
地址：https://mjixiang.github.io/vue-pagebar


##输入
```
	*page:Number 当前页 必须
	*recordCount:Number 总记录数 若 == false 则不显示分页条
	*psize:Number 页大小默认20
	*changeEvent:String 可选 默认onPageChange 页码发生变化冒泡的方法名(若同一页面需要使用多个分页，需指定changeEvent避免事件监听冲突，如本例)
```

##事件捕获
```javascript
	//父组件
	events:{
		//处理页码变化后的事件（默认`onPageChange`） 若指定了changeEvent则捕获对应的事件
		onPageChange(p){
	  		//do something 一般请求后台数据	
		}	
	}
```
