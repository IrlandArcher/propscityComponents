<template>
<!-- 购物车 -->
  <div class="app-shop">
    <!--1.图片轮播-->
    <div class="mui-card">
			<div class="mui-card-content">
				<div class="mui-card-content-inner">
					<swiper-box :list="imglist"></swiper-box>
				</div>
			</div>
		</div>  
    <!--2.商品列表-->
    <div class="mui-card">
      <div class="mui-card-header">商品列表</div>
			<div class="mui-card-content">
				<div class="mui-card-content-inner">
				  <!--2.1 mui  左侧图片  右侧文字-->
          <ul class="mui-table-view">
				    <li class="mui-table-view-cell mui-media" v-for="item in cartlist" :key="item.id">
					    <a href="javascript:;">
						    <img class="mui-media-object mui-pull-left" src="">
						    <div class="mui-media-body">
							    {{item.title}}
							   <p class='mui-ellipsis'>
                   <span class="price">{{item.price}}</span>
                   <span class="count">
                     <!--2.2mui 数字按钮-->
                     <div class="mui-numbox" data-numbox-min='1' data-numbox-max='9'>
					             <button class="mui-btn mui-btn-numbox-minus" type="button" @click="getSub(item.id)">-</button>
					             <input id="test" class="mui-input-numbox" type="number" :value="item.count" />
					             <button class="mui-btn mui-btn-numbox-plus" type="button" @click="getAdd(item.id)">+</button>
				             </div>
                   </span>
                 </p>
						    </div>
					    </a>
				    </li>
          </ul> 
					<div>合计：{{getSubTotal}} 蓝色精粹</div> 		
				</div>
			</div>
		</div>    
  </div>
</template>
<script>
//引入子组件
import swiper from "../sub/swiper.vue"
//注册当前组件
//在模板中调用轮播图组件
//data声明数组件

  export default {
    data(){
      return{
				imglist:[],
				cartlist:[],
			}  
    },
		methods:{
			getSub(id){//传入商品参数id
			//	console.log("-"+id);//测试
			  //1.获取数组中每个元素
				for(var item of this.cartlist){
					//2.判断参数中id与当前元素id是否相同
					if(item.id==id){
						if(item.count<2)
							return;
						//3.当前元素数量+1
						item.count--;
						break;
					}
				}
				//
				this.val--;
			},
			getAdd(id){
			//	console.log("+"+id) //测试
			 //1.获取数组中每个元素
				for(var item of this.cartlist){
					//2.判断参数中id与当前元素id是否相同
					if(item.id==id){
						//3.当前元素数量+1
						item.count++;
						break;
					}
				}
			},
			getImageList(){
				this.$http.get("imagelist").then(result=>{
					this.imglist=result.body;
				})
			},
			getCartList(){
				this.$http.get("shopCart").then(result=>{
					this.cartlist=result.body;
				})
			},
		
		},
    created(){
      //console.log(this.$route.query.id) //查询字符串传参
      //console.log(this.$route.params.id)
			this.getImageList();
			this.getCartList();
    },
		components:{
			"swiper-box":swiper,
		},
		computed:{
			getSubTotal:function(){
				//计算商品价格累加和并返回
				//1.创建临时变量
				var sum=0;
				//2.创建循环
				for(var item of this.cartlist){
					//3.计算累加和
					sum += item.price*item.count;
				}
				//4.返回累加结果
				return sum;
			}
		},
  }  
</script>
<style>
    
</style>