<template>
    <div class="app-newslist">
        <ul class="mui-table-view">
            <li class="mui-table-view-cell mui-media" v-for="item in list" :key="item.id">
                <router-link :to="`/home/newsInfo?id=`+item.id">
                    <img class="mui-media-object mui-pull-left" :src="item.img_url">
                    <div class="mui-media-body">
                        {{item.title}}
                        <p class='mui-ellipsis'>
                            <span>{{ item.ctime  | datetimeFilter }}</span>
                            <span>点击： {{item.point}} 次</span>
                        </p>
                    </div>
                </router-link>
            </li>
            <mt-button type="primary" size="large" @click="getMore">加载更多</mt-button>
        </ul>
    </div>
</template>
<script>
    export default {
        data(){
            return {
                list:[],
                pageIndex:0,          //属性显示当前页数 
                pageSize:5,           //页大小
                hasMore:true,         //是否存在下一页数据
                pageCount:1,          //总页数           
            }
        },
        methods:{//加载更多
            getMore(){   
                this.pageIndex++;
                //判断是否有下一页数据
                this.hasMore = this.pageIndex <= this.pageCount;
                //如果没有，阻止执行函数
                if(!this.hasMore){return} 
                var url = "http://127.0.0.1:3000/newslist";
                url+="?pno="+this.pageIndex+"&pageSize="+this.pageSize
                this.$http.get(url).then(result=>{
                    //vue resource ajax
                    //concat 拼接数组 将第二个数组拼接到新数组
                 var rows=this.list.concat(result.body.data);
                 this.list = rows;
                 //保存总页数
                 this.pageCount= result.body.pageCount   
                })
            }
        },
        created(){
            this.getMore();
        }
    }
</script>
<style>
    .app-newslist .mui-table-view li .mui-ellipsis{
        display:flex;          /*父元素设置弹性布局 */
        font-size:12px;         
        color:#226aff;
        justify-content:space-between; /*两端对齐 */
    }
</style>