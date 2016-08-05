# vue-pagebar
A paging component for Vue.js

基于Vue.js的分页组件

[查看jquery版本](https://github.com/mjixiang/ui.paging)

##example
地址：https://mjixiang.github.io/vue-pagebar


##props
```html
<Paging :page.sync="page" :record-count="recordCount" :psize="20"></Paging>
```

>`page`:`Number` 当前页，必须，双向绑定

>`recordCount`:`Number` 总记录数，若 `== false` 则不显示分页条

>`psize`:`Number` 页大小，默认`20`

>`changeEvent`:`String` 页码发生变化父组件需监听的方法名，可选，默认`onPageChange` 

>>(若同一页面需要使用多个分页，需指定`changeEvent`避免事件监听冲突，如本示例)

##events
```javascript
//父组件中
events:{
	//处理页码变化后的事件（默认`onPageChange`） 若指定了changeEvent则捕获对应的事件
	onPageChange(p){
  		//do something 一般页码p请求对应页码数据
	}	
}
```
