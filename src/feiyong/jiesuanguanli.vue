<template>
  <div id="jiesuan">
    <div class="jiesuan" v-if="chaxun">
      <div class="content">
        <input type="text" v-model="cha">
        <button @click='fn'>查询</button>
      </div>
    </div>
    <div class="jiesuan_" v-if="!chaxun">
      <div class="chaxun">
        <input type="text" name='number' v-model="cha">
        <button @click='fn'>查询</button>
      </div>
      <div class="table">
        <table cellspacing="0" cellpadding="0">
          <tr>
            <th>
              <input type="checkbox" />
              <span>租赁方式</span>
            </th>
            <th>客户姓名</th>
            <th>电话号码</th>
            <th>车型</th>
            <th>证件类型</th>
            <th>证件号码</th>
            <th>取车时间</th>
            <th>操作</th>
          </tr>
          <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
          </tr>
          <tr v-for="(item,index) in jiesuan" :key="index">
            <td>
              <input type="checkbox" />
              <span v-text="item.leaseWay"></span>
            </td>
            <td v-text="item.userName"></td>
            <td v-text="item.phone"></td>
            <td v-text="item.carType"></td>
            <td v-text="item.cardType"></td>
            <td v-text="item.cardId"></td>
            <td v-text="item.quDate"></td>
            <td>
              <div>
                <img src="./../../static/img/shouli.png" />
                <span style="color:#0a82e1" @click='shouli(3,1)'>受理</span>
              </div>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chaxun:true,
      cha:'',
      jiesuan: [
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        },
        {
          name: "邱士长",
          phone: 17621322007,
          zuping: "国内租",
          chexing: "经济型",
          zj: "身份证",
          zjh: 411300167803194414,
          time: "2019-05-01"
        }
      ]
    };
  },
  methods: {
    shouli(num, tab) {
      this.$store.commit("changetabnum", num);
      this.$store.commit("changetabtab", tab);
      if (
        this.$store.state.tag.name.indexOf(
          this.$store.state.Tab.Tab_[num - 1].tits[tab].tit
        ) == -1
      ) {
        this.$store.state.tag.tag_.push({
          name: this.$store.state.Tab.Tab_[num - 1].tits[tab].tit,
          url: this.$store.state.Tab.Tab_[num - 1].tits[tab].href,
          num: this.$store.state.Tab.num,
          tab: this.$store.state.Tab.tab,
          head: this.$store.state.Tab.Tab_[num - 1].tits[tab].head
        });
        this.$store.state.tag.name.push(
          this.$store.state.Tab.Tab_[num - 1].tits[tab].tit
        );
      }
      this.$store.commit(
        "changetaglight",
        this.$store.state.Tab.Tab_[num - 1].tits[tab].head
      );
      this.$router.push('/index/shouliyuding');
    },
    fn(){
      console.log(this.$store.state.IP)
      this.chaxun=false;
      this.$axios.get(this.$store.state.IP+'/leaserecord/getAll?number='+this.cha).then((res)=>{
        console.log(res);
        this.jiesuan=res.data.leaserecordList;
      })
    }
  },
  components: {}
};
</script>

<style scoped lang='less'>
#jiesuan {
  width: 100%;
  height: 100%;
  .jiesuan {
    margin-left: 50px;
    margin-top: 50px;
    width: 1182px;
    height: 685px;
    background: rgba(255, 255, 255, 0.85);
    .content {
      margin-left: 255px;
      padding-top: 278px;
      input {
        width: 398px;
        height: 60px;
        background: transparent;
        outline: none;
        border: 1px solid #bbb;
        font-size: 16px;
        text-indent: 20px;
      }
      button {
        margin-left: 90px;
        width: 211px;
        height: 54px;
        background: #fc0;
        border: none;
        border-radius: 5px;
        color: #fff;
        font-size: 24px;
        cursor: pointer;
      }
    }
  }
  .jiesuan_ {
    margin-top: 50px;
    margin-left: 50px;
    width: 1182px;
    height: 720px;
    background: rgba(255, 255, 255, 0.85);
    .chaxun {
      padding-left: 24px;
      padding-top: 118px;
      margin-bottom: 32px;
      input {
        border: 1px solid #bbb;
        width: 315px;
        height: 40px;
        font-size: 16px;
        text-indent: 15px;
        outline: none;
      }
      button {
        margin-left: 68px;
        width: 156px;
        height: 40px;
        border: none;
        outline: none;
        background: #fc0;
        color: #fff;
        font-size: 24px;
        border-radius: 5px;
        cursor: pointer;
      }
    }
    .table {
      position: relative;
      width: 1141px;
      max-height: 260px;
      display: flex;
      margin-left: 12px;
      overflow-y: auto;
      overflow-x: hidden;
      border: 3px solid #e2e3e3;
      &::-webkit-scrollbar {
        display: none;
      }
      &::-webkit-scrollbar-button {
        display: none;
      }
      &::-webkit-scrollbar-track {
        display: none;
      }
      table {
        width: 100%;
        height: 100%;
        text-align: center;
        tr {
          color: #fff;
          font-size: 20px;
          &:nth-child(2n) {
            background: #eceded;
          }
          &:nth-child(2n + 1) {
            background: #fff;
          }
          &:nth-child(n + 1) {
            height: 42px;
            line-height: 42px;
          }
          &:first-child {
            height: 47px;
            line-height: 47px;
            background: #0099ff;
            position: fixed;
          }
          &:nth-child(2) {
            height: 47px;
            line-height: 47px;
          }
          th {
            font-weight: normal;
            border-left: 3px solid #e2e3e3;
            &:nth-child(1) {
              border: none;
              width: 136px;
              span {
                display: block;
                float: right;
                width: 80px;
                margin-right: 10px;
              }
            }
            &:nth-child(2) {
              width: 112px;
            }
            &:nth-child(3) {
              width: 136px;
            }
            &:nth-child(4) {
              width: 76px;
            }
            &:nth-child(5) {
              width: 122px;
            }
            &:nth-child(6) {
              width: 210px;
            }
            &:nth-child(7) {
              width: 142px;
            }
            &:nth-child(8) {
              width: 186px;
            }
          }
          td {
            font-size: 18px;
            color: #666;
            border-left: 3px solid #e2e3e3;
            &:nth-child(1) {
              border: none;
              width: 136px;
              span {
                display: block;
                float: right;
                width: 80px;
                margin-right: 10px;
              }
            }
            &:nth-child(2) {
              width: 114px;
            }
            &:nth-child(3) {
              width: 136px;
            }
            &:nth-child(4) {
              width: 76px;
            }
            &:nth-child(5) {
              width: 122px;
            }
            &:nth-child(6) {
              width: 210px;
            }
            &:nth-child(7) {
              width: 142px;
            }
            &:last-child {
              overflow: hidden;
        cursor: pointer;
            }
          }
        }
      }
    }
  }
}
@media all and (min-width: 681px) and (max-width: 1366px) {
  .jiesuan {
    height: 445px !important;
  }
  #jiesuan .jiesuan .content[data-v-9fcc8924] {
    margin-left: 235px !important;
    padding-top: 170px !important;
  }
  .jiesuan_ {
    width: 97% !important;
    height: 446px !important;
  }
  .chaxun {
    padding-top: 20px !important;
  }
  .table {
    width: 96% !important;
    max-height: 300px !important;
  }
  #jiesuan .jiesuan_ .table table tr th[data-v-9fcc8924]:nth-child(8) {
    width: 125px !important;
  }
  #jiesuan .jiesuan_ .table table tr th[data-v-9fcc8924]:nth-child(2) {
    width: 114px !important;
  }
}

</style>
