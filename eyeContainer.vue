<template>
    <div>
        <div class="mui-content">
			<div class="mui-card">
				<div class="mui-card-content">
					<div class="mui-card-content-inner">
						<ul class="fl">
                            <li>排序</li><span class="mui-icon mui-icon-arrowdown"></span>
                            <li>分类</li><span class="mui-icon mui-icon-arrowdown"></span>
                            <li>过滤</li><span class="mui-icon mui-icon-arrowdown"></span>
                        </ul>   
					</div>
				</div>
			</div>
        </div> 
         <div class="app-skinslist">
            <div class="skins-item" v-for="item in list" :key="item.id">
            <img :src="item.img_url" @click="getDetail(item.id)"/>
            <h3 class="title">{{item.title}}</h3>
            <div class="info">
                <p class="price">
                <span class="now">{{item.now}}</span>
                <span class="old">{{item.old}}</span>
                </p> 
                <p class="sell">
                <span>{{item.onsale}}</span>
                <span>剩 {{item.q}}件</span>
                </p>  
            </div>
    </div>  
  </div> 
    </div>
</template>

<script>
   export default {
        data(){
            return{
              list:[
              {id:1,title:"太空蜥蜴",now:"1999点券",old:"3999",onsale:"限时热卖中",q:"298",img_url:"http://127.0.0.1:3000/img/eye_1.jpg"},
              {id:2,title:"太空守卫",now:"3666点券",old:"5888",onsale:"爆热抢手",q:"359",img_url:"http://127.0.0.1:3000/img/eye_2.jpg"},
              {id:3,title:"全息真视",now:"4888点券",old:"8888",onsale:"即将断货",q:"159",img_url:"http://127.0.0.1:3000/img/eye_3.jpg"},
              {id:4,title:"混沌鹰眼",now:"3666点券",old:"7888",onsale:"上新打折",q:"228",img_url:"http://127.0.0.1:3000/img/eye_4.jpg"},
              {id:5,title:"太空战机",now:"1999点券",old:"3999",onsale:"限时热卖中",q:"398",img_url:"http://127.0.0.1:3000/img/eye_5.jpg"},
              {id:6,title:"星星守卫",now:"3666点券",old:"5888",onsale:"爆热抢手",q:"259",img_url:"http://127.0.0.1:3000/img/eye_6.jpg"},
              {id:7,title:"死兆星之握",now:"4888点券",old:"8888",onsale:"即将断货",q:"169",img_url:"http://127.0.0.1:3000/img/eye_7.jpg"},
              {id:8,title:"源·火眼",now:"3666点券",old:"7888",onsale:"上新打折",q:"208",img_url:"http://127.0.0.1:3000/img/eye_8.jpg"}
              ]
            }
        },
        methods:{
         
        },
    }
</script>
<style>
   .fl{
       display: flex;
       justify-content: space-around;
       list-style: none;
   }
</style>