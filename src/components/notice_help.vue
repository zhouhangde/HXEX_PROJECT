<template>
    <div class="notice clr-part" style="overflow:hidden">
        <!-- <indexHeader></indexHeader> -->
        <div class="account-wrap" style="width:1200px;margin:60px auto;">
            <div class="account" style="width:auto">
                <div>
                    <!-- <div class="back-nav  ft20 clear" style="padding:0 20px;">{{$t('header.help')}}</div> -->
                    
                </div>
                <div class="account-content">
                    <div class="tc hide" style="padding-top: 150px;">
                        <img src="../assets/images/nodata.png" alt=""> 
                        <p class="fColor2 ft18">{{$t('nodata')}}</p>
                    </div>
                    <div>
                        <ul class="noticeList">
                            <li class="clear curPer bdr-part" v-for="item in newList" :key="item.id">
                                <div class=""  @click="goDetail(item.thisid)">
                                        <div class="">{{item.title}}</div>
                                        <span class="fr">{{item.time}}</span>
                                    
                                </div>
                            </li>
                        </ul> 
                    </div>
                    <div class="tc" style="padding:15px">
                        <!-- <div class="fColor1 ft14 mt10" @click="getMore">{{more}}</div> -->
                        <!-- <div>
                            <img src="@/assets/images/loading.gif" alt=""  class="lodw20">
                            <p class="ft12 baseColor">加载中...</p>
                        </div> -->
                    </div>
                </div>
             </div>
        </div>
    </div>
</template>
<script>
import indexHeader from "@/view/indexHeader";
export default {
  name: "noticeList",
  components: { indexHeader },
  data() {
    return {
      more: "点击加载更多...",
      newList: [],
      id:''
    };
  },
  props:{
    // header 标题
    title:{
      type:String,
      default:'公告',
    },
     
  },
  created() {
      this.id = this.$route.query.id || '';
  },

  methods: {
    getNotice(){
      this.$http({
        url:  '/api/news/notice_center',
        method:'get',
        // params:{c_id:this.id}
        // data:{language:this.$i18n.locale == 'zh'?1:2}
      }).then(res => {
        var that = this;
        // //console.log(res);
        this.newList=res.data.message;
        $.each(this.newList,function(k,v){
          v.time = that.timestampToTime(v.time);
        })
      })
    },
    
    goBefore() {
      this.$router.back(-1);
    },
    getMore() {
      //console.log(123);
    },
    goDetail(id) {
      var id = id;
      this.$router.push({
        name: "noticeDetail",
        query: { id: id }
      });
    },
    timestampToTime(timestamp) {
            var date = new Date(timestamp); //时间戳为10位需*1000，时间戳为13位的话不需乘1000
            var Y = date.getFullYear() + '-';
            var M = (date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1) + '-';
            var D = this.change(date.getDate()) + ' ';
            var h = this.change(date.getHours()) + ':';
            var m = this.change(date.getMinutes()) + ':';
            var s = this.change(date.getSeconds());
            return Y + M + D + h + m + s;
        },
        change(t) {
            if (t < 10) {
                return "0" + t;
            } else {
                return t;
            }
        }
  },
  mounted(){
      var that = this;
      that.getNotice();
    }
};
</script>
<style lang="scss" scoped>
.notice {
  overflow: hidden;
  .account-wrap {
    // background: url(../assets/images/account_center_bg.jpg) no-repeat;
    // background-size: cover;
    .account {
      // width: 1500px;
      margin: 0 auto;
      // padding-top: 30px;
      overflow: hidden;
      // min-height: 880px;
      padding-top: 0;
      .back-nav {
        height: 40px;
        font-size: 16px;
        line-height: 40px;
      }
      .nav-after {
        display: block;
        height: 10px;
        background-color: #262a42;
      }
      .account-content {
        width: 100%;
        min-height: 450px;
        // background-color: #fff;
        ul {
          padding: 0 20px;
          font-size: 14px;
          li {
            border-bottom: 1px dashed #eee;
            // height: 72px;
            padding: 10px 0 7px;
            // color: #333;
                font-size: 12px;
            > div {
              > div {
                height: 36px;
                line-height: 18px;
              }
              span{
                  color: #61688a;
              }
            }
          }
          li:hover{
            color: #de5959;
          }
        }
      }
    }
  }
}
</style>

