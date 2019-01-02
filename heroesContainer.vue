<template>
<div id="app-heroesList">
  <!--英雄列表-->
    <ul class="mui-table-view">
      <li class="mui-table-view-cell mui-media" v-for="item in list" :key="item.id" @click="adpoint">
        <router-link :to="'/heroes?id='+item.id">
            <img class="mui-media-object mui-pull-left" :src="item.img_url">
            <div class="mui-media-body">
                {{item.title}}
                <p>{{item.hdesc}}</p>
                <p class='mui-ellipsis'>
                  <span>{{item.ctime|datetimeFilter}}</span>
                  <span>点击次数{{item.point}}</span>
                </p>
            </div>
        </router-link>
      </li>
    </ul>
    <!--加载更多是实现原先de保留，新内容添加在原有de后面-->
    <mt-button type="primary" size="large" @click="getMore">加载更多</mt-button>  
</div>  
</template>
<script>
  export default {
    data(){
        return{
        list:[],
        pageIndex:0,  
        pageSize:5,  
        hasMore:true, 
        pageCount:1  
        }
    },
    methods:{
        getMore(){
          this.pageIndex++;
          this.hasMore = this.pageIndex <= this.pageCount;
          if(!this.hasMore){return}
          var url="http://127.0.0.1:3000/heroes";
          url+="?pno="+this.pageIndex+"&pageSize="+this.pageSize;
          this.$http.get(url).then(result=>{
             var rows=this.list.concat(result.body.data);
             this.list=rows;  
             this.pageCount=result.body.pageCount;
          })
        },
        adpoint(){
          this.item.point++;
        }
    },
    created(){
        this.getMore();
    }
  }  
</script>
<style>
#app-heroesList .mui-table-view li .mui-ellipsis{
    display:flex; 
    font-size:12px;
    color:#226aff;
    justify-content:space-between;
} 
</style>