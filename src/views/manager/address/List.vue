<template>
 <briup-fulllayout title="常用地址">
    <!--{{addresses}}-->
    <van-list>
    <van-cell
        v-for="item in addresses"
        :key="item"
        :title="item.province+' '+item.city+' '+item.area+' '+item.address"
    />
    </van-list>
    <br>
   
    <van-button block type="default" @click="toAddressEditHandler" color="linear-gradient(to right, #db70db, #70dbdb)">添加</van-button>
 </briup-fulllayout>
</template>
<script>
import {get} from '../../../http/axios'
import {mapState} from 'vuex'
    export default {
    data(){
        return{
        addresses:[]
        }

    },
    
        computed:{
            //将状态机中的user对象中的info对象获取到
            ...mapState("user",["info"])
        },

    created(){
        //调用加载地址方法
this.loadAddress();
    },
    methods:{
        loadAddress(){
            let id = this.info.id;
            let url = "/address/findByCustomerId?id="+id;
            get(url).then((reponse)=>{
                this.addresses = reponse.data;
            })
        },
        toAddressEditHandler(){
            this.$router.push("/manager/address_edit");
          }
        }
    }
</script>