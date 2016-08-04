<style scoped>
	/*分页*/
	.paging-box{box-shadow:3px 0 8px #ccc;}
	.page-bar{text-align:center;}
	.page-items{margin:15px 0px 5px 0px;padding:0px;border-radius:4px;display:inline-block;}
	.page-items>li{color:#428bca;border:1px solid #dddddd;background-color:white;padding:5px 10px;font-size:12px;float:left;margin-left:-1px;position:relative;display:block;line-height:1.5em;cursor:pointer;}
	.page-current-item{color:white!important;background-color:#428bca!important;border-color:#428bca;cursor:default!important;}
	.page-disable-item{color:#999!important;background-color:white!important;border-color:#ddd;cursor:default!important;pointer-events:none;}
	.page-jump{display:inline-block;height:28px;font-size:14px;margin-left:20px;color:#428bca;-webkit-transform:translate(0,-16px);-moz-transform:translate(0,-16px);-ms-transform:translate(0,-16px);-o-transform:translate(0,-16px);transform:translate(0,-16px);}
	.page-jump input{width:50px;padding:0px;margin:0px;height:27px;text-align:center;border:1px solid #ccc;color:#428bca;}
	.page-jump button{width:50px;padding:0px;margin:0px;height:29px;border:1px solid #ccc;background:white;margin-left:5px;cursor:pointer;color:#428bca;}
</style>
<template>
	<div v-show="pages.length" class="paging-box">
		<div class="page-bar">
			<ul class="page-items">
				<li @click="setPage(1)" :class="{'page-disable-item':page == 1}">首页</li>
				<li @click="setPage(page-1)" :class="{'page-disable-item':page == 1}">上一页</li>
				<li v-for="p in pages" @click="setPage(p)" :class="{'page-current-item':p == page}">{{ p }}</li>
				<li @click="setPage(page+1)" :class="{'page-disable-item':page == maxPage}">下一页</li>
				<li @click="setPage(maxPage)" :class="{'page-disable-item':page == maxPage}">末页</li>
			</ul>
			<div class="page-jump">
				<span>共{{ maxPage }}页</span>
				<input type="number" v-model="jumpPage" min="1" :max="maxPage">
				<button @click="setPage(jumpPage)" class="page-goto">确定</button>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data(){
		return {
			jumpPage:this.page
		}
	},
	computed:{
		maxPage(){
			return Math.ceil(this.recordCount / this.psize);
		},
		pages(){
			if(!this.maxPage) return [];
			var pages = [];
			if (this.page > this.maxPage - 3) {
				for (var i = Math.max(1, this.maxPage - 6); i <= this.page - 4; i++) {
					pages.push(i);
				}
			}
			for (var i = 1; i <= this.maxPage; i++) {
				if (this.page - 3 <= i && i <= this.page + 3) {
					pages.push(i);
				}
			}
			if (this.page < 4) {
				for (var i = 4 + this.page; i <= Math.min(7, this.maxPage); i++) {
					pages.push(i);
				}
			}
			return pages;
		}
	},
	watch:{
		page(val){
			this.jumpPage = this.page;
			this.$dispatch(this.changeEvent,val);
		}
	},
	methods:{
        setPage(p){
        	p = p < 1 ? 1 : p > this.maxPage ? this.maxPage : p;
        	this.page = p;
        }
    },
	props:{
		page:{
			type:Number,
			default:0,
			twoWay:true,
			coerce(val){
				return val*1;
			}
		},
		psize:{
			type:Number,
			default:20
		},
		recordCount:{
			type:Number,
			default:0,
			coerce(val){
		        return val*1;
		    }
		},
		changeEvent:{
			type:String,
			default:'onPageChange'
		}
	}
}
</script>