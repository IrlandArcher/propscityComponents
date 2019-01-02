<template>
  <div id="app-homeContainer">
    <hr/>
      <!--轮播图-->
      <mt-swipe :auto="3000">
        <mt-swipe-item v-for="item in list" :key="item.id"><img :src="item.img_url"></mt-swipe-item>
      </mt-swipe>
      <hr/>
      <!-- 六宫格 --> 
      <ul class="mui-table-view mui-grid-view mui-grid-9">
        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/heroes">
                <img src="../../img/menu1.jpg"/>
                <div class="mui-media-body">英雄</div></router-link></li>
        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/home/skinslist">
                <img src="../../img/menu2.jpg"/>
                <div class="mui-media-body">皮肤</div></router-link></li>
        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/eye">
                <img src="../../img/menu3.jpg"/>
                <div class="mui-media-body">守卫/图标</div></router-link></li>
        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/photo">
                <img src="../../img/menu4.jpg"/>
                <div class="mui-media-body">礼包</div></router-link></li>
        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/deriva">
                <img src="../../img/menu6.jpg"/>
                <div class="mui-media-body">周边</div></router-link></li>
        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
                <img src="../../img/menu5.jpg"/>
                <div class="mui-media-body"> 。。。</div></a></li>
      </ul> 
      <!-- 最新上架 -->
      <div class="mui-card">
        <div class="mui-card-content">
          <p style="margin:0">最新上架</p>
          <div class="mui-card-content-inner" style="display:flex;padding:0 ">
              <div style="margin:3px">
                <img src="http://127.0.0.1:3000/img/pkg-mm.jpg" style="width:228px;height:166px" />
              </div>
              <div style="margin:3px">
                <img src="http://127.0.0.1:3000/img/pkg-xp.jpg" style="width:113px;height:80px"/>
                <img src="http://127.0.0.1:3000/img/pkg-nw.jpg" style="width:113px;height:80px"/>
              </div>
          </div>
        </div>
      </div>
      <!-- 什么值得买 --> 
      <div class="mui-card">
        <div class="mui-card-content">
          <p style="margin:0"> 什么值得买</p>
          <div class="mui-card-content-inner" style="margin:3px;display:flex;padding:0">
            <div class="wtb">
                <p class='wtb_p'>什么值得买：震惊！想为..</p>
                <img src="http://127.0.0.1:3000/img/2-9009-9.jpg" alt="">img-00
            </div>
            <div class='wtb'>
                <p class='wtb_p'>什么值得买：经典永不落..</p>
                <img src="http://127.0.0.1:3000/img/2-20006-9.jpg" alt="">img-00
            </div>
          </div>
        </div>
      </div>
      <!-- 推荐英雄 -->
      <div class="mui-card">
        <div class="mui-card-content">
          <p style="margin:0">推荐英雄</p>
          <div class="mui-card-content-inner">
            <img class='tj_img' src="http://127.0.0.1:3000/img/big39000.jpg" alt="">刀锋舞者 艾瑞莉娅 
          </div>
        </div>
      </div>
      <!-- 推荐皮肤 -->
      <div class="mui-card">
        <div class="mui-card-content">
          <p style="margin:0">推荐皮肤</p>    
          <div class="mui-card-content-inner">
              <img class='tj_img' src="http://127.0.0.1:3000/img/big39006.jpg" alt="">玉剑传说 舞剑仙
          </div>
        </div>
      </div>
      <!-- 推荐周边 -->
      <div class="mui-card">
        <div class="mui-card-content">
          <p style="margin:0">推荐周边</p>
          <div class="mui-card-content-inner">
              <img class='tj_img' src="http://127.0.0.1:3000/img/corn.jpg" alt=""> 2018年冠军纪念币
          </div>
        </div>
      </div>        
  </div>
</template>

<script>
export default {
      data(){
          return{
            list:[]  
          }
      },
      methods:{
        getImage(){
          //发送ajax请求并且获得图片列表并显示
          var url="http://127.0.0.1:3000/imagelist";
          this.$http.get(url).then(result=>{
            this.list=result.body  
          })
        },
      },
      mounted() {
         //mui.init();
         this.getImage();
      },
      created(){
      }
  }  
</script>
<style>
 
  #app-homeContainer .mint-swipe{
      height:143px;
  }
  #app-homeContainer .mint-swipe img{
      width:100%;
  }
  /*跳转九宫格*/  
  #app-homeContainer .mui-grid-view.mui-grid-9{
    background:#fff;
    border:0;
  }
  .mui-grid-view.mui-grid-9 img{
    width:60px;
    height:60px;
  }
  #app-homeContainer .mui-table-view.mui-grid-view .mui-table-view-cell .mui-media-body{
    font-size:15px;
  }
  .mui-card-content-inner{
    margin-left: 0;
    padding-left: 0;
  }
  .wtb{
    margin:3px;
    width:170px;
    height:165px;
  }
  .wtb_p{
    text-align:center;
    vertical-align:center;
  }
  .tj_img{
    margin-left: 0px;
    width:355px;
  }
</style>