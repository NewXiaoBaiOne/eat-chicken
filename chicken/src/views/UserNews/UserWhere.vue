<template>
  <div class="userwhere">
    <header class="userwhere-head">
      <div class="userwhere-head-box">
        <div class="userwhere-head-return">
          <img
            src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMCIgaGVpZ2h0PSIzMiI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTE2LjU1MiA1LjYzM0wxNC41MDggMy41OSAyLjI0MyAxNS44NTMgMTQuNTA4IDI4LjQxbDIuMDQ0LTIuMDQzLTEwLjIyLTEwLjUxM3oiLz48L3N2Zz4="
            alt=""
          />
        </div>
        <h1>我的地址</h1>
      </div>
    </header>
    <div class="userwhere-box">
      <div class="userwhere-box2">
        <div
          class="userwhere-content"
          v-for="data of userWhere"
          :key="data.addressid"
        >
          <div class="userwhere-news">
            <p class="userwhere-news-top">
              <span class="userwhere-name">{{ data.name }}</span>
              <span class="userwhere-sex">{{ data.usersex }}</span>
              <span class="userwhere-phone">{{ data.phone }}</span>
            </p>
          </div>
          <div class="userwhere-control">
            <i class="iconfont icon-xiugai" @click="modifyAddress(data)"></i>
            <i class="iconfont icon-cha" @click="delAddress(data)"></i>
          </div>
        </div>
        <div class="userwhere-control btn-addAdress">
          <router-link to="/user/addwhere">新增地址</router-link>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import bus from "@/bus";
export default {
  data() {
    return {
      userId: 0,
      userWhere: [],
    };
  },
  created() {
    this.userId = localStorage.getItem("userID");
    console.log("UserId:", this.userId);
    this.updataAddress();
  },
  methods: {
    updataAddress() {
      this.userWhere = [];
      this.$axios
        .post("http://localhost:1234/user/address")
        .then((res) => {
          for (let linS of res.data) {
            if (linS.userid == this.userId) this.userWhere.push(linS);
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },
    modifyAddress(dataM) {
      localStorage.setItem("modifyID", dataM.addressid);
      this.$router.push("/user/modify");
    },
    delAddress(dataM) {
      console.log("modifyID", dataM.addressid);
      this.$axios
        .post("http://localhost:1234/user/deladdress", {
          addressid: dataM.addressid,
        })
        .then((res) => {
          console.log(res.data);
          this.updataAddress();
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  beforeMount() {},
};
</script>
<style lang="less" scoped>
.userwhere {
  height: 11.73vw;
  .userwhere-head {
    z-index: 100;
    top: 0;
    left: 0;
    background-image: linear-gradient(90deg, #0af, #0085ff);
    .userwhere-head-box {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 11.73vw;
      height: 11.73vw;
      .userwhere-head-return {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 11.73vw;
        height: 11.73vw;
        img {
          width: 3.2vw;
          max-width: 100%;
        }
      }
      h1 {
        height: 11.73vw;
        color: #fff;
        top: 0;
        left: 50%;
        max-width: 50%;
        position: absolute;
        white-space: nowrap;
        overflow: ellipsis;
        font-weight: 700;
        font-size: 5vw;
        line-height: 11.73vw;
        transform: translateX(-50%);
      }
    }
  }
  .userwhere-box {
    min-width: 100%;
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    .userwhere-box2 {
      position: relative;
      overflow-y: auto;
      padding-bottom: 10.86vw;
      .btn-addAdress {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        bottom: 0;
        a {
          width: 35vw;
          height: 8vw;
          font-size: 5vw;
          text-align: center;
          font-weight: 700;
          display: block;
          border-radius: 2vw;
          background-color: #4bdfdf;
          &:hover {
            background-color: #3190e8;
          }
        }
      }
    }
  }
}
.userwhere-content {
  width: 100%;
  float: left;
  padding: 0 0 4vw;
  border-bottom: 0.33vw solid #ddd;
  background-color: #fff;
  border-top: 0.26vw solid #ddd;
  .userwhere-news {
    width: 75%;
    height: 100%;
    float: left;
    margin-top: 2vw;
    margin-left: 2vw;
    overflow: hidden;
    .userwhere-news-top {
      font-size: 4.66vw;
      margin: 0;
      color: #666;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      margin-bottom: 1.06vw;
      .userwhere-name {
        color: #333;
        font-weight: 700;
      }
      .userwhere-sex {
        padding: 0 1.6vw 0 0.8vw;
      }
    }
    .userwhere-news-bottom {
      color: #666;
      font-size: 3.73vw;
      margin: 0;
      display: flex;
      align-items: center;
      .userwhere-label {
        font-size: 2.66vw !important;
        position: relative;
        flex: none;
        color: #3190e8;
        display: inline-block;
        white-space: nowrap;
        margin-right: 0.8vw;
        padding: 0.53vw;
        border-radius: 0.13vw;
        line-height: 2.66vw;
        border: 1px solid #3190e8;
      }
      .userwhere-label-school {
        border-color: #00d762;
        color: #00d762;
      }
      .userwhere-label-home {
        border-color: #ff5722;
        color: #ff5722;
      }
      .userwhere-where {
        line-height: 4.53vw;
        margin: 0;
      }
    }
  }
  .userwhere-control {
    width: 20%;
    height: 100%;
    flex-basis: 13.06vw;
    margin-top: 2vw;
    float: right;
    justify-content: space-between;
    align-items: center;
    i {
      height: 4.8vw;
      width: 4.8vw;
      margin-left: 2vw;
      line-height: 11vw;
    }
  }
}
</style>