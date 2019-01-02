<template>
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
</template>
<script>
//练习：1.依据list列表创建模板中的商品
//练习：2.点击商品图片跳转GoodInfo.vue传递参数
    export default {
        data(){
            return{
              list:[
              {id:1,title:"电锯魔蝎",now:"1999点券",old:"3999",onsale:"限时热卖中",q:"298",img_url:"http://127.0.0.1:3000/img/skin1.jpg"},
              {id:2,title:"未来战士",now:"3666点券",old:"5888",onsale:"爆热抢手",q:"359",img_url:"http://127.0.0.1:3000/img/skin2.jpg"},
              {id:3,title:"源·双枪",now:"4888点券",old:"8888",onsale:"即将断货",q:"159",img_url:"http://127.0.0.1:3000/img/skin3.jpg"},
              {id:4,title:"源·鹰眼",now:"3666点券",old:"7888",onsale:"上新打折",q:"308",img_url:"http://127.0.0.1:3000/img/skin4.jpg"}
              ]
            }
        },
        methods:{
          getDetail(id){
          //参数：商品id
            //console.log(id)
            this.$router.push("/home/skinsinfo/"+id);
          }
        },
    }
</script>
<style>
.app-skinslist{
    display:flex;    /*最外层设置弹性布局 */
    flex-wrap:wrap;  /*子元素换行*/
    justify-content:space-between;/*两端对齐*/
    padding:7px;    /*为子元素内补丁*/
}    
.app-skinslist .skins-item{
    width:49%;               /*元素宽度*/
    border:1px solid #ccc;   /*边框*/
    box-shadow:0 0 8px #ccc; /*阴影*/
    margin:4px 0;
    padding:2px;
    display:flex;
    flex-direction:column;
    justify-content:space-between;
    min-height:293px;        /*最小高度*/

}
.app-skinslist .skins-item img{
    width:100%;
}
.app-skinslist .skins-item .now{
    color:red;
    font-weight:bold;
    font-size:16px;
}
.app-skinslist .skins-item .old{
    font-size:12px;
    margin-left:10px;
    text-decoration:line-through;
}
</style>