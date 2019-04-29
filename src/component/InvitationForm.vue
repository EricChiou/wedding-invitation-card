<template>
  <div id="invitation-form-container">
    <div class="content">
      <div class="title">邀請單</div>
      <div class="option">
        <div class="sub-title">姓名：</div>
        <input>
      </div>
      <div class="option">
        <div class="sub-title">人數：</div>
        <input type="number" min="0" placeholder="請填數字">
      </div>
      <div class="option">
        <div class="sub-title">素食：</div>
        <input type="number" min="0" placeholder="請填數字">
      </div>
      <div class="option">
        <div class="sub-title">手機：</div>
        <input>
      </div>
      <div class="option">
        <div class="sub-title">Email：</div>
        <input>
      </div>
      <div class="option">
        <div class="sub-title">Line：</div>
        <input>
      </div>
      <div>
        *請至少留一項聯絡方式
        <br>
        <br>
      </div>
      <div class="option-relation">
        <div class="sub-title">與新人關係：</div>
        <input class="radio" type="radio" name="relation" value="男方">男方親友
        <input class="radio" type="radio" name="relation" value="女方">女方親友
      </div>
      <div class="option-paper">
        <div class="sub-title">紙本喜帖：</div>
        <input class="radio" type="radio" name="paper" value="true">是
        <input class="radio" type="radio" name="paper" value="false" checked>否
      </div>
      <div class="option-address">
        <div class="sub-title">地址：</div>
        <input>
      </div>
      <div class="option-other">
        有其他需求或有什麼話想對我們說嗎：
        <br>
        <textarea></textarea>
      </div>
      <div class="send">
        <button>送出</button>
      </div>
    </div>
    <img class="bg" src="../assets/images/join_bg.jpg">
    <img class="bg-m" src="../assets/images/join_bg_m.jpg">
  </div>
</template>

<script>
export default {};
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
    height: 840px;
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
