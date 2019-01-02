<template>
  <div>
		<h3><img class='logo' src="http://127.0.0.1:3000/img/lol.jpg" width="40px" height="40px" alt="...">因为热爱  所以联盟</h3>
    <form action="#">
      用户名：<input type="text" name="uname" placeholder="请输入QQ账户" v-model="unameval"> <br>
      密码：<input type="password" name="upwd"  placeholder="请输入密码" v-model="upwdval"> <br>
      <input type="button" id="btn" value="登录" @click="btnSubmit">
    </form>
  </div>  
</template>
<script>
  import {Toast} from "mint-ui";
  export default {
    data(){
      return{
        unameval:"",
        upwdval:"",
      }  
    },
    methods:{
      btnSubmit(){
        var u = this.unameval;
        var p = this.upwdval;
        //console.log(u+"-"+p);
        this.$http.get("login?uname="+u+"&upwd="+p).then(result=>{
          if(result.body.code==1){
            Toast(result.body.msg)
            this.$router.push("/");
          }else
            Toast(result.body.msg);
        })
      }
    }
  }  
</script>
<style>
    .logo{
      position:absolute;
      left:330px;
      top:50px;
    }
</style>