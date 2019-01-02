<template>
  <div class="app-subswipe">
    <!--图片轮播-->
    <mt-swipe :auto="3000">
      <mt-swipe-item v-for="item in list" :key="item.id"><img :src="item.img_url" /></mt-swipe-item>
    </mt-swipe>
  </div>
</template>
<script>
  export default {
      data(){
        return{  }
      },
      props:["list"],
  }  
</script>
<style>
/*轮播图高宽设置*/
.app-subswipe .mint-swipe{
    height:143px;
}
.app-subswipe .mint-swipe img{
    width:100%;
}

</style>>