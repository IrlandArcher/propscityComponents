<template>
    <div class="app-newinfo">
      <h3>{{news.title}}</h3>
      <div>{{news.content}}</div> 
      <!--保存评论子组件 3.调用子组件-->
      <comment-box :id="this.id"></comment-box>
    </div>  
</template>
<script>
  //1.引入子组件
  import comment from "../sub/comment.vue";
  export default {
    data(){
        return{
          news:{},
          id:this.$route.query.id,    
        }
    },
    methods:{
        getNews(){  //发送ajax请求获取当前新闻详细信息
          var url="http://127.0.0.1:3000/newsinfo";
          this.$http.get(url).then(result=>{
              this.news=result.body;
          })  
        },
    },
    created(){
        this.getNews();
    },
    //2.注册子组件
    components:{
        "comment-box":comment,
    },
  }  
</script>
<style>
    
</style>