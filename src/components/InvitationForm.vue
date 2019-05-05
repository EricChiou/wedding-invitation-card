<template>
  <div id="invitation-form-container" style="display:none;">
    <div class="content">
      <div class="title">邀請單</div>
      <div class="option">
        <div class="sub-title">姓名：</div>
        <input v-model="apply.name">
      </div>
      <div class="option">
        <div class="sub-title">人數：</div>
        <input type="number" min="0" placeholder="請填數字" v-model="apply.number">
      </div>
      <div class="option">
        <div class="sub-title">素食：</div>
        <input type="number" min="0" placeholder="請填數字" v-model="apply.vegetarian">
      </div>
      <div class="option">
        <div class="sub-title">手機：</div>
        <input v-model="apply.phone">
      </div>
      <div class="option">
        <div class="sub-title">Email：</div>
        <input v-model="apply.email">
      </div>
      <div class="option">
        <div class="sub-title">Line：</div>
        <input v-model="apply.line">
      </div>
      <div>
        *請至少留一項聯絡方式
        <br>
        <br>
      </div>
      <div class="option-relation">
        <div class="sub-title">與新人關係：</div>
        <input class="radio" type="radio" name="relation" value="男方親友" v-model="apply.relation">男方親友
        <input class="radio" type="radio" name="relation" value="女方親友" v-model="apply.relation">女方親友
      </div>
      <div class="option-paper">
        <div class="sub-title">紙本喜帖：</div>
        <input class="radio" type="radio" name="paper" value="true" v-model="apply.card">是
        <input class="radio" type="radio" name="paper" value="false" checked v-model="apply.card">否
      </div>
      <div class="option-address">
        <div class="sub-title">地址：</div>
        <input v-model="apply.address">
      </div>
      <div class="option-other">
        有其他需求或有什麼話想對我們說嗎：
        <br>
        <textarea v-model="apply.other"></textarea>
      </div>
      <div class="send">
        <button v-if="!loading" @click="send">送出</button>
        <button v-if="loading" disabled>傳送中</button>
      </div>
    </div>
    <img class="bg" src="../assets/images/join_bg.jpg">
    <img class="bg-m" src="../assets/images/join_bg_m.jpg">
    <div v-if="showDialog" @click="close">
      <Dialog v-bind:message="message"></Dialog>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import Dialog from './Dialog.vue';

export default {
  components: { Dialog },
  data: () => ({
    apply: {
      name: '',
      number: 0,
      vegetarian: 0,
      phone: '',
      email: '',
      line: '',
      relation: '',
      card: false,
      address: '',
      other: ''
    },
    loading: false,
    message: '',
    showDialog: false
  }),
  methods: {
    send() {
      this.apply.number = Number(this.apply.number);
      this.apply.vegetarian = Number(this.apply.vegetarian);
      this.apply.card = this.apply.card === 'true';
      if (this.loading) {
        return;
      }
      if (!this.apply.name) {
        this.message = '請輸入姓名';
        this.showDialog = true;
        return;
      }
      if (!this.apply.number) {
        this.message = '請輸入人數';
        this.showDialog = true;
        return;
      }
      if (!this.apply.phone && !this.apply.email && !this.apply.line) {
        this.message = '請至少留一項聯絡方式';
        this.showDialog = true;
        return;
      }
      if (!this.apply.relation) {
        this.message = '請選擇與新人關係';
        this.showDialog = true;
        return;
      }
      if (this.apply.card && !this.apply.address) {
        this.message = '請留喜帖寄送地址';
        this.showDialog = true;
        return;
      }
      this.loading = true;
      axios
        .post(`https://${window.location.hostname}:6200/apply/add`, this.apply)
        .then(resp => {
          if (resp.data.result === 'success') {
            this.message = '送出完成';
          } else {
            console.log(resp);
            this.message = '送出失敗';
          }
          this.showDialog = true;
          this.loading = false;
        })
        .catch(error => {
          console.error(error);
          this.message = '送出失敗';
          this.loading = false;
        });
    },
    close(event) {
      if (
        event.target.className === 'mask' ||
        event.target.className === 'confirm'
      ) {
        this.showDialog = false;
      }
    }
  }
};
</script>


<style lang="scss" scoped>
#invitation-form-container {
  display: inline-block;
  position: relative;
  height: 555px;
  z-index: 999;
  .content {
    position: absolute;
    top: 14%;
    right: 15%;
    left: 15%;
    bottom: 15%;
    text-align: left;
    color: #ad2839;
    .title {
      margin-bottom: 10px;
      font-size: 28px;
      font-weight: bold;
      text-align: center;
    }
    .option {
      display: inline-block;
      margin: 0 15px 15px 0;
      width: calc(33% - 14px);
      .sub-title {
        width: 56px;
        display: inline-block;
      }
      input {
        width: calc(100% - 69px);
        padding: 3px 5px;
        border: 1px solid rgb(169, 169, 169);
        border-radius: 4px;
      }
      @media only screen and (max-width: 767px) {
        display: block;
        width: 100%;
      }
    }
    .option-relation {
      margin: 0 15px 15px 0;
      .sub-title {
        display: inline-block;
        width: 100px;
      }
      @media only screen and (max-width: 767px) {
        .sub-title {
          display: block;
          margin-bottom: 5px;
        }
      }
    }
    .option-paper {
      display: inline-block;
      margin: 0 15px 15px 0;
      width: calc(33% - 14px);
      .sub-title {
        width: 100px;
        display: inline-block;
      }
      @media only screen and (max-width: 767px) {
        width: 100%;
        .sub-title {
          display: block;
          margin-bottom: 5px;
        }
      }
    }
    .option-address {
      display: inline-block;
      margin: 0 15px 15px 0;
      width: calc(66% - 13px);
      .sub-title {
        display: inline-block;
        width: 56px;
      }
      input {
        width: calc(100% - 69px);
        padding: 3px 5px;
        border: 1px solid rgb(169, 169, 169);
        border-radius: 4px;
      }
      @media only screen and (max-width: 767px) {
        display: block;
        width: calc(100% - 14px);
        input {
          margin-top: 2px;
          width: 100%;
        }
      }
    }
    .option-other {
      textarea {
        width: calc(100% - 34px);
        height: 80px;
        margin-top: 2px;
        padding: 3px 5px;
        resize: none;
        border-radius: 4px;
        @media only screen and (max-width: 767px) {
          width: calc(100% - 14px);
        }
      }
    }
    .send {
      margin-top: 5px;
      text-align: center;
      button {
        padding: 6px 8px;
        font-size: 18px;
        font-weight: bold;
        font-family: Microsoft JhengHei;
        color: #ffffff;
        background-color: #d08490;
        border: none;
        border-radius: 4px;
        cursor: pointer;
      }
    }
  }
  .bg {
    display: inline-block;
    width: 100%;
    height: 100%;
  }
  .bg-m {
    display: none;
  }

  @media only screen and (max-width: 767px) {
    height: 880px;
    .content {
      top: 9%;
      .title {
        font-size: 26px;
      }
    }
    .bg {
      display: none;
    }
    .bg-m {
      display: inline-block;
      width: 100%;
      height: 100%;
    }
  }
}
</style>
