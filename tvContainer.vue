<template>
    <div id="app-tvContainer">
         <div class="mui-content">
			<div class="mui-card">
				<div class="mui-card-content">
					<div class="mui-card-content-inner">  
                        <mt-swipe :auto="3000">   
                            <mt-swipe-item v-for="item in list" :key="item.id"> 
                                <h4>
                                    今日推荐<span class="mui-badge mui-badge-warning mui-badge-inverted">{{item.id}}</span><span class="mui-badge mui-badge-inverted">/ 3</span>
                                </h4>
                                <img :src="item.img_url" >
                                <div>{{item.title}}</div>
                            </mt-swipe-item>  
                        </mt-swipe>
					</div>
                    <hr />
                    <div class="mui-card-content-inner">
                        <h4>新片速递<span class="mui-badge mui-badge-warning">New</span></h4>
                        <div class="mui-badge mui-badge-warning title_div"><h4><span class="mui-icon mui-icon-bars"></span> 克烈：重逢</h4> </div>
                        <div class='video_div'>
                            <video class='video' src="http://127.0.0.1:3000/video/Kled.mp4" autoplay controls muted preload loop ></video>
                        </div>
                    </div>
                    <hr />
                    <div class="mui-card-content-inner">
                        <h4>皮肤介绍<span class="mui-badge mui-badge-warning">New</span></h4>
                        <div class="mui-badge mui-badge-warning title_div"><h4><span class="mui-icon mui-icon-bars"></span> 未来战士:伊泽瑞尔</h4> </div>
                        <div class='video_div'>
                            <video class='video' src="http://127.0.0.1:3000/video/Ezreal.mp4" autoplay muted preload loop ></video>
                        </div>
                    </div>
                     <hr />
                    <div class="mui-card-content-inner">
                        <h4>赛事频道<span class="mui-badge mui-badge-warning">共 1 场</span></h4>
                        <div class="mui-badge mui-badge-warning title_div"><h4><span class="mui-icon mui-icon-bars"></span> 赛事回放</h4> </div>
                        <div class='video_div'>
                            <video class='video' src="http://127.0.0.1:3000/video/Kled.mp4"  controls preload  ></video>
                        </div>
                    </div>
				</div>
			</div>
        </div>  
    </div>
</template>
<script>
     export default {
        data(){
            return{
                list:[],
               
            }
        },
        methods:{
            getImage(){
            //发送ajax请求并且获得图片列表并显示
                var url="http://127.0.0.1:3000/video_imglist";
                this.$http.get(url).then(result=>{
                    this.list=result.body 
                    console.log(result.body); 
                })
            },
        },
        mounted() {
            this.getImage();      
        },
        created(){
        }
    }   
</script>
<style> 
 #app-tvContainer .mint-swipe{
      height:244px;
  }
#app-tvContainer .mint-swipe img{
    width:100%;
}
.fl{
    display: flex;
    justify-content: space-around;
    list-style: none;
}
img{
    border-radius: 5%;
}
hr{
    width:85%;
    height: 0.05px;
    margin: 0 25px;
}
.title_div{
    width:100%;
    height:35px;
    border-radius: 5%;
    margin-bottom: 10px;
    margin-top:0;
   
}
.video{
    width:325px;
    margin-left:0;
}
</style>