<template>
  <div class="app-comment">
    <h3>发表评论</h3>
    <hr>
    <textarea placeholder="请吐槽，最多120字" maxlength="120" v-model="msg"></textarea>
    <mt-button size="large" @click="postComment">发表评论</mt-button>
    <div class="cmt-list">
      <div class="cmt-item" v-for="(item,i) in list" :key="item.id">
        <div class="cmt-info">
          <h4>第{{i+1}}楼</h4>
          用户:{{item.user_name}} <span>发表时间:{{item.ctime|datetimeFilter}}</span>
        </div>
        <div class="cmt-body">
          {{item.content}}
        </div>
      </div>
      <mt-button type="primary" size="large" @click="getComment">加载更多</mt-button>
    </div>
  </div>
</template>
<script>
import{Toast} from "mint-ui";
  export default {
    data(){
      return{
        msg:"",  //双向绑定用户评论，用于获得评论数据
        list:[],
        pageIndex:0, //当前页码
        pageSize:5,  //页大小
        hasMore:true
      }  
    },
    props:["id"],
    methods:{
      postComment(){
        //1.获取新闻编号
        var nid=this.id;
        //2.获取评论内容
        var pmsg=this.msg;
        //3.判断新闻评论内容不能为空,提示用户
        if(pmsg.trim().length==0){  //trim()去掉左右边空格
          Toast("评论内容不能为空！")
          return;
        }
        //4.发送post请求
        var url="http://127.0.0.1:3000/postcomment";
        this.$http.post(url,{nid:nid,msg:pmsg}).then(result=>{
          //console.log(result); 
          //5.获取服务器程序返回
          //6.提示用户"评论成功"
          Toast("发表成功!");
          //清空pageIndex
          this.pageIndex=0;
          this.list=[];
          this.getComment(); 
        }) 
         console.log('cmt');      
      },
      getComment(){
          //1.页码自增
          this.pageIndex++;
          //判断是否有下一页数据
          this.hasMore=this.pageIndex <= this.pageCount;
          //如果没有下一页数据停止函数的执行
          if(!this.hasMore){return};
          //2.发送ajax请求，
          var pno=this.pageIndex;
          var s=this.pageSize;
          var id=this.id;
          console.log(this);
          var url="getcomment?id="+id+"&pno="+pno+"&pageSize="+s;
          //console.log(p+":"+s+":"+id)
          this.$http.get(url).then(result=>{
             var rows=this.list.concat(result.body.data);
             this.list=rows;
            //  this.pageCount=result.body.pageCount;
          })  
        },  
    },
    created(){
       this.getComment();  
    }
  }  
</script>  
<style>
.app-comment .mui-table-view li .mui-ellipsis{
    color:#226aff;
    text-align:right;
}  
.app-comment h3{ /*评论组件 */
  font-size:15px;
} 
.app-comment textarea{ /*评论组件多行文本框 */
  font-size:14px;
  height:85px;
  margin:0;
}
.app-comment .cmt-list{ /*评论列表 */
  margin:5px 0; /*顶部和前面元素间距 */
}
.app-comment .cmt-list .cmt-info{
  font-size:12px;
  font-family:"yahei";
  line-height:25px;
  background:pink;
}
.app-comment .cmt-list .cmt-info img{
  width:25px;
  height:25px;
  vertical-align:bottom;
}
.app-comment .cmt-list .cmt-info span{
  font-size:9px;
 
}
.app-comment .cmt-list .cmt-body{
  background:#fff;
  line-height:30px;
  text-indent:2em;
}
</style>