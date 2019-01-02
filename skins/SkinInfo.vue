<template>
  <div class="app-skininfo">
    <!--商品轮播区域-->
    <div class="mui-card">
	  <div class="mui-card-content">
		<div class="mui-card-content-inner">
          <!--3.调用子组件-->
          <swiper-box :list="imglist"></swiper-box>   
		</div>				
	  </div>
	</div>
    <!--商品购买区域-->
    <div class="mui-card">
	  <div class="mui-card-header">{{skininfo.title}}</div>
	  <div class="mui-card-content">
		<div class="mui-card-content-inner">
          <p class="price">
            市场价：<del class="old">{{skininfo.old}}</del>
            销售价：<span class="now">{{skininfo.now}}</span>
          </p>
        
            购买数量：
          <div class="mui-numbox" data-numbox-min='1' data-numbox-max='9'>
            <button class="mui-btn mui-btn-numbox-minus" type="button" @click="skinSub">-</button>
            <input id="test" class="mui-input-numbox" type="number" value="1" v-model="val"/>
            <button class="mui-btn mui-btn-numbox-plus" type="button" @click="skinAdd">+</button>
          </div>
      
          <p>
            <mt-button type="primary" size="small">购买至本区</mt-button>

            <mt-button type="primary" size="small">赠送给好友</mt-button>
            
            <mt-button type="danger" size="small" @click="addCartTo()">加入购物车</mt-button>
          </p>
		</div>
	  </div>
	  <div class="mui-card-footer">结账请移步上方购物车，谢谢！</div>
	</div>
    <!--商品参数-->
    <div class="mui-card">
	  <div class="mui-card-header">商品参数</div>
	  <div class="mui-card-content">
		<div class="mui-card-content-inner">
		  <p>商品货号：{{skininfo.pid}}</p>	
          <p>商品名称：{{skininfo.title}}</p>
          <p>商品颜色：紫藤红</p>
          <p>市场价格：<del>{{skininfo.old}}</del>蓝色精粹</p>
          <p>优惠价格：{{skininfo.now}}蓝色精粹</p>
          <p>商品运费：免运</p>
		</div>
	  </div>
	  <div class="mui-card-footer">页脚</div>
	</div>
  </div>
  
</template>
<script>
    import {Toast} from "mint-ui";
    /*在父组件引入子组件步骤：1.引入2.注册 3.调用  */
    //1.引入轮播图组件
    import swiper from "../sub/swiper.vue";
    //引入mui.js库 引入报错，因为Vue脚手架是启动严格模式，mui.js是早期的，里面存在一些不是严格模式的代码。
    //解决方案：Ⅰ.按装第三方插件禁止脚手架严格模式————babel-plugin-transform-remove-strict-mode
    //Ⅱ.不用mui.js文件，自己写触发事件
    //import mui from "../../lib/mui/js/mui.js";


    export default {
        data(){
            return{
              imglist:[],
              skininfo:{},
              val:1,
            }
        },
        methods:{
          getImage(){
            var url="imagelist";
            this.$http.get(url).then(result=>{
              this.imglist=result.body;
              //console.log(result)
            })  
          },
          skinAdd(){
            if(this.val<=998)  
            this.val++;  
          },
          skinSub(){
            if(this.val>1)
            this.val--;  
          },
        //服务器数据：返回模拟数据[id;title;now;old;商品编号]
          getGoodInfo(){
            //商品列表将商品id传递商品详情
            var id=this.$route.params.id  
            var url="skinsinfo?id="+id;
            this.$http.get(url).then(result=>{
                this.skininfo=result.body;
                console.log(result.body);
            })  
          },
          //将商品添加至购物车
          addCartTo(){
            //console.log("添加购物车") //测试
            //1.将商品编号和数量保存到服务器
             //1.1获取商品编号
               var id=this.$route.params.id;  
             //1.2获取商品数量
               var count=this.val;
             //  console.log(id+"-"+count);
               
             //1.3发送请求
             this.$http.get("addCart?pid="+id+"&count="+count).then(result=>{
               if(result.body.code==1){
                 Toast(result.body.message);
                 //1.4更新购物车中商品数量———修改Vuex共享数据
                 this.$store.commit("increment",count);
                 //共享数据保存现阶段不能刷新，localStore浏览器自带对象，永久保存
               }else{
                 Toast(result.body.message);
               };
             })
            //2.更新App.vue组件购物车数量
          },
        },
        created(){
          //console.log(this.$route.params.id)
          this.getImage();
          this.getGoodInfo();
        },
        components:{
          "swiper-box":swiper, //2.子组件注册
        }
    }
</script>
<style>
.mui-card .price .old{
    margin-right:50px;
}
.mui-card .price .now{
    color:red;
    font-size:16px;
    font-weight:bold;
}   
</style>