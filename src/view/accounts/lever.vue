<template>
    <div class="lever bgf8">
        <div class="lever-head">
            <span>净资产折合:</span> 
            <span>{{total}} USDT</span>
            <span class="ft12 mincny">≈{{total_cny}} CNY</span>
            <!-- <input type="checkbox" class="ml20">
            <span class="ft14">隐藏小额资产</span>
            <input type="text" class="filter-input ml20"> -->
            <span class="fr ">财务记录</span>
        </div>
        <div class="leverbody contentBK ft12">
            <ul class="titlebox  clearfix">
                <li class="w25">杠杆账户</li>
                <li class="w25 tr">可用</li>
                <li class="w25 tr">冻结</li>
                <li class="w25 tr">折合(CNY)</li>
                <!-- <li class="w11 tr">风险率</li>
                <li class="w5 tr">爆仓价</li> -->
                <!-- <li class="w25 tr">操作</li> -->
            </ul>
            <ul class="contentbox ">
                <li class="clearfix flex" v-for="(item,index) in list" :key="index">
                    <p class="w25 l40">{{item.currency_name}}</p>
                    <p class="w25 tr flex column center">
                        <span>{{item.balance}}</span>
                        <!-- <span>0.00000000 USDT</span> -->
                    </p>
                    <p class="w25 tr flex column center">
                        <span>{{item.lock_balance}}</span>
                        <!-- <span>0.00000000 USDT</span> -->
                    </p>
                    <p class="w25 tr flex column between">
                        <span>{{item.rate_balance}}</span>
                        <span>≈ {{item.usdt_balance}}(USDT)</span>
                    </p>
                    <!-- <p class="w11 tr l40">无风险</p>
                    <p class="w5 tr l40">---</p> -->
                    <!-- <p class="w25 tr  l40 btn"> -->
                        <!-- <span @click="turnin">转入</span>
                        <span @click="turnout">转出</span> -->
                        <!-- <span @click="golever">杠杆</span> -->
                    <!-- </p> -->
                </li>
                <!-- <li class="clearfix flex">
                    <p class="w11 l40">BTC/USDT</p>
                    <p class="w16 tr flex column between">
                        <span>0.00000000 BTC</span>
                        <span>0.00000000 USDT</span>
                    </p>
                    <p class="w16 tr flex column between">
                        <span>0.00000000 BTC</span>
                        <span>0.00000000 USDT</span>
                    </p>
                    <p class="w16 tr flex column between">
                        <span>0.00000000 BTC</span>
                        <span>0.00000000 USDT</span>
                    </p>
                    <p class="w11 tr l40">无风险</p>
                    <p class="w5 tr l40">---</p>
                    <p class="w25 tr  l40 btn">
                        <span @click="turnin">转入</span>
                        <span @click="turnout">转出</span>
                        <span>杠杆</span>
                    </p>
                </li> -->
            </ul>
            <!-- <div class="tc ft16  mt50">暂无数据</div> -->
        </div>
        <div class="dialog_wrap" v-show="inDialog">
            <div class="dialog">
                <div class="dia-tit clearfix">
                    <span class="fl ">转入本金</span>
                    <span class="fr  close" @click="close">X</span>
                </div>
                <div class="dia-content ">
                    <div class="dia-container">
                        <div class="flex alcenter frombox">
                            <span class=" ft12 tc">从</span>
                            <p class="ft14 flex1">交易账户</p>
                        </div>
                        <div class="frombox flex alcenter w10 tc">
                            <img src="@/assets/images/trade.png" alt="" class="coinimg">                      
                        </div>
                        <div class="flex alcenter frombox">
                            <span class=" ft12 tc">到</span>
                            <p class="ft14 flex1">BTC/USDT杠杆账户</p>
                        </div>
                    </div>
                    <div class="div-input mt20">
                        <p class="ft12 ">币种</p>
                        <div class="dia-coin flex tc mt10 ft12 ">
                            <p v-for="(item,index) in coins" :class="{select:index==current}" @click="chooseCoin(index)">{{item.coin}}<i></i></p>
                        </div>
                    </div>
                    <div class="div-input mt20">
                        <p class="ft12  flex between">
                            <span>数量</span>
                            <span>可转 0.00000000 BTC</span>
                        </p>
                        <div class="inputboxs flex between alcenter mt10">
                            <input type="text">
                            <div class="ft12 ">
                                <span>BTC</span>
                                <span>|</span>
                                <span class="all">全部</span>
                            </div>
                        </div>
                    </div>
                    <div class="btn-box flex ft16 tc">
                        <div>取消</div>
                        <div class="sure">确定</div>
                    </div>
                </div>
            </div>
        </div>
        <div class="dialog_wrap" v-show="outDialog">
            <div class="dialog">
                <div class="dia-tit clearfix">
                    <span class="fl ">转出本金</span>
                    <span class="fr  close" @click="close">X</span>
                </div>
                <div class="dia-content ">
                    <div class="dia-container">
                        <div class="flex alcenter frombox">
                            <span class=" ft12 tc">从</span>
                            <p class="ft14 flex1">BTC/USDT杠杆账户</p>
                        </div>
                        <div class="frombox flex alcenter w10 tc">
                            <img src="@/assets/images/trade.png" alt="" class="coinimg">                      
                        </div>
                        <div class="flex alcenter frombox">
                            <span class=" ft12 tc">到</span>
                            <p class="ft14 flex1">交易账户</p>
                        </div>
                    </div>
                    <div class="div-input mt20">
                        <p class="ft12 ">币种</p>
                        <div class="dia-coin flex tc mt10 ft12 ">
                            <p v-for="(item,index) in coins" :class="{select:index==current}" @click="chooseCoin(index)">{{item.coin}}<i></i></p>
                        </div>
                    </div>
                    <div class="div-input mt20">
                        <p class="ft12  flex between">
                            <span>数量</span>
                            <span>可转 0.00000000 BTC</span>
                        </p>
                        <div class="inputboxs flex between alcenter mt10">
                            <input type="text">
                            <div class="ft12 ">
                                <span>BTC</span>
                                <span>|</span>
                                <span class="all">全部</span>
                            </div>
                        </div>
                    </div>
                    <div class="btn-box flex ft16 tc">
                        <div>取消</div>
                        <div class="sure">确定</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import indexHeader from '@/view/indexHeader'
export default {
    name:'lever',
    data(){
        return{
            current:0,
            inDialog:false,
            outDialog:false,
            coins:[{coin:"ETC"},{coin:"USDT"}],
            list:[],
            total:'',
            total_cny:''
        }
    },
    components:{indexHeader},
    methods:{
        chooseCoin(index){
           this.current=index;
        },
        turnin(){
            this.inDialog=true
        },
        turnout(){
            this.outDialog=true
        },
        close(){
            this.inDialog=false
            this.outDialog=false
        },
        golever(){
            this.$router.push({name:'manger'})
        },
        getInfo(){
            this.$http({
            url: '/api/' + 'wallet/info',
            method:'get',
            data:{},
            headers: {'Authorization':  this.token},
            }).then(res=>{
                if(res.data.type == 'ok'){
                    this.list = res.data.message.lever.balance;
                    this.total = res.data.message.lever.total;
                    this.total_cny = res.data.message.lever.total_rate
                }              
            })
        }
    },
    created(){
        this.token= localStorage.getItem('token') || '';
        //console.log(this.address);
        this.getInfo();
        // if(this.address){
        //     this.$http({
        //         url:'/api/'+'money/rechange?user_id='+this.address,
        //         type:'GET'
        //     }).then(res=>{
        //         //console.log(res)
        //         this.addr=res.data.message.company_eth_address;
        //         this.url='http://qr.liantu.com/api.php?&w=300&text='+res.data.message.company_eth_address;
        //         var content = this.addr;
        //         var clipboard = new Clipboard('#copy')
        //     }).catch(error=>{
        //         return error
        //     })
        // }
    },
    mounted(){
        // this.init();
    }
};
</script>
<style scoped lang="scss">
.lever{
    height: 820px;
    .lever-head{
        // background-color: #1b1e2e;
        padding: 0 30px;
        height: 48px;
        line-height: 48px;
        font-size: 16px;
        // color: #c7cce6;
        .mincny{
            color: #61688a;
        }
        .filter-input{
                display: inline-block;
                width: 125px;
                height: 28px;
                padding: 0 30px 0 10px;
                background: none;
                border-radius: 3px;
                border: 1px solid #ccc;
        }
    }
    .leverbody{
        padding: 0 20px;
        .titlebox{
            height: 40px;
            line-height: 40px;
            li{
                float: left;
            }
        }
        .contentbox{
            li{
                height: 60px;
                padding:10px;
                border-bottom: 1px solid #ccc;
                >p{
                    float: left;
                    height: 40px;
                }
                .l40{
                    line-height: 40px
                }
                .btn{
                    span{
                        margin-left: 20px;
                        cursor: pointer;
                    }
                    span:hover{
                        color: #61688a
                    }
                }
            }
        }
    }
    .dialog_wrap {
        position: fixed;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        z-index: 9;
        text-align: center;
        // background: rgba(0,0,0,.4);
        .dialog {
            margin-top: 220px;
            display: inline-block;
            width: 560px;
            padding-top: 30px;
            box-sizing: border-box;
            border-radius: 3px;
            text-align: left;
            vertical-align: middle;
            // background-color: #262a42;
            .dia-tit{
                padding: 0 40px 30px;
                font-size: 24px;
                line-height: 24px;
                .close{
                    cursor: pointer;
                }
                .close:hover{
                    // color: #fff
                }
            }
            .dia-content{
                padding: 0 40px;
                margin-bottom: 20px;
                .frombox{
                    height: 48px;
                    line-height: 48px;
                    span{width: 10%}
                    p{
                        height: 48px;
                        padding-left: 20px;
                        line-height: 48px;
                        border-radius: 3px;
                        // background-color: #202437;
                    }
                    .coinimg{
                        width: 28px;
                        margin: 0 auto
                    }
                }
                .dia-coin{
                    // background-color: #202437;
                    p{
                        width: 50%;
                        width: 50%;
                        height: 48px;
                        line-height: 48px;
                        cursor: pointer;
                        position: relative;
                        i{
                            display: none;
                            position: absolute;
                            bottom: 4px;
                            right: 4px;
                            width: 0;
                            height: 0;
                            border: 6px solid transparent;
                            border-right: 6px solid #fff;
                            border-bottom: 6px solid #fff;
                        }
                    }
                    .select{
                        color: #fff;
                        background-color: #7a98f7;
                        i{
                            display: block
                        }
                    }
                    p:first-child{
                        border-radius: 3px 0 0 3px;
                    }
                    p:last-child{
                        border-radius: 0 0px 3px 0;
                    }
                } 
                .inputboxs{
                    width: 100%;
                    border-radius: 3px;
                    // background-color: #1e2235;
                    border: 1px solid #ccc;
                    padding: 0 20px;
                    input{
                        background: transparent;
                        height: 46px;
                        // color: #fff

                    }
                    span{
                        margin-left: 15px
                    }
                    .all{
                        color: #ff7519;
                        cursor: pointer;
                    }
                }
                .btn-box{
                    margin: 50px 0;
                    div{
                        width: 50%;
                        height: 48px;
                        line-height: 48px;
                        margin: 0 10px;
                        border-radius: 3px;
                        cursor: pointer;
                    }
                    .sure{
                        color: #fff;
                        background: #7a98f7;
                    }
                }
                
            }
        }
            
    }
}
</style>


