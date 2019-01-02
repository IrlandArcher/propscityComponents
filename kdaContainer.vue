<template>
    <div id='kdaContainer'>
         <div class="mui-content">
			<div class="mui-card">
				<div class="mui-card-content">
					<div class="mui-card-content-inner sign-in-box" v-for="item in list" :key="item.id">
                        <h4>{{item.area}}<a><span class="mui-icon mui-icon-pulldown"></span></a></h4>
                        <img class="avatar" :src="item.img_url" alt="头像">
                        <p>{{item.uname}}<span class="mui-badge mui-badge-purple">{{item.lever}}</span></p>
                        <p>{{item.state}}</p>    
                    </div>
                </div>
                <div class="mui-card-content">
					<div class="mui-card-content-inner score-box">
                        <h4>战绩</h4>
                        <h4>能力</h4>
                        <h4>资产</h4>
                    </div>
                </div>
                <div class="mui-card-content">
					<div class="mui-card-content-inner">
                        <div>段位</div>
                        <div class="score-box">总局数 x  胜率  y%
                            <div>超神</div>
                            <div>五杀</div>
                            <div>四杀</div> 》
                        </div>
                    </div>
                </div>  
                 <div class="mui-card-content mission">
					<div class="mui-card-content-inner score-box">
                       <p>游戏任务</p>
                       <p>每日首胜 <img class="suc_icon" src="http://127.0.0.1:3000/img/boosts_1.jpg" alt="">  》</p>  
                    </div>
                </div>    
                 <div class="mui-card-content">
					<div class="mui-card-content-inner">
                        <h4>全部战绩</h4>
                        <ul class="mui-table-view" v-for="item in kdalist" :key="item.id">
                            <li class="mui-table-view-cell mui-media"  >
                                <!-- <router-link> -->
                                    <img class="mui-media-object mui-pull-left" :src="item.img_url">
                                    <div class="mui-media-body">
                                        <p> 
                                            <span>(结果)  击杀/助攻/死亡</span>
                                            <span> 时间</span>      
                                        </p>
                                        <p class='mui-ellipsis'>
                                            <span>游戏模式</span>
                                            <span>友</span>
                                        </p>
                                    </div>
                                <!-- </router-link> -->
                            </li>
                        </ul>
                        <mt-button type="primary" size="large" @click="getKda" v-if="hasMore">加载更多</mt-button> 
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
                kdalist:[],
                pageIndex:0,  
                pageSize:5,  
                hasMore:true, 
                pageCount:1  
            }
        },
        methods:{
            getAvatar(){
                var url="http://127.0.0.1:3000/kda_list";
                this.$http.get(url).then(result=>{
                    this.list=result.body;
                    console.log(result.body); 
                })
            },
            getKda(){
                this.pageIndex++;
                this.hasMore = this.pageIndex <= this.pageCount;
                if(!this.hasMore){return}
                var url="http://127.0.0.1:3000/heroes";
                url+="?pno="+this.pageIndex+"&pageSize="+this.pageSize;
                this.$http.get(url).then(result=>{
                var rows=this.kdalist.concat(result.body.data);
                this.kdalist=rows;  
                this.pageCount=result.body.pageCount;
                }) 
            }
        },
        mounted() {
            this.getAvatar();    
        },
        created(){
             this.getKda()
        }
    }   
</script>
<style> 
  .mui-badge .mui-badge-purple{
      position: absolute;
      left:-150px;
      bottom:100px;
  }
  .sign-in-box{
    background-color:aquamarine;
    text-align: center;
    margin: 30px;
    margin:0;
    padding:0;
   }
   .avatar{
       width:78px;
       height:78px;
       border-radius: 50%;
   }
   .score-box{
    display: flex;
    justify-content: space-between;
   }
   .suc_icon{
       width:15px;
       height:15px;
   }
   .mission{
       margin:0;
       padding:0;
   }
</style>