<template>
  <div class="app-photo">
    <!--mui card--> 
    <div class="mui-card">
	  <div class="mui-card-content">
		<div class="mui-card-content-inner">
		  <ul class="photo-list">
            <li v-for="item in imglist" :key="item.id">
              <img v-lazy="item.img_url" /> <!--v-lazy是一个属性-->
            </li>
      </ul>
		</div>
	  </div>
	</div>
  </div>
</template>
<script>
  export default {
    data(){
      return {
        imglist:[],  
      }  
    },
    methods:{
      getImglist(){
        this.$http.get("imagelist").then(result=>{
            this.imglist=result.body;
            //console.log(result);
        })

      }  
    },
    created(){
      this.getImglist();  
    },
  }  
</script>
<style>
.photo-list{
  padding:0;
  background:#999;
  list-style: none;
}  
.photo-list li img{
  width:100%;  
}
.photo-list li img[lazy=loading]{
  width:100%;
  height:100%; 
  margin:auto;  
}
</style>