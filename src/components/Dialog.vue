<template>
  <div id="dialog-container">
    <div class="mask"></div>
    <div class="message-container">
      <div class="message-block">
        <div class="message-content">
          <div class="background">
            <img src="../assets/images/dialog.png">
          </div>
          <div class="message">
            <div class="inline-block height-100"></div>
            <div class="inline-block">
              <div class="text">{{this.message}}</div>
              <button class="confirm">確認</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    message: String
  }
};
</script>

<style lang="scss" scoped>
#dialog-container {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 99999;
  .mask {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.6);
  }
  .message-container {
    position: absolute;
    top: 200px;
    right: 0;
    left: 0;
    text-align: center;
    animation: fall 0.6s;
    .message-block {
      display: inline-block;
      width: 320px;
      height: 180px;
      .message-content {
        position: relative;
        width: 100%;
        height: 100%;
        .background,
        .message {
          position: absolute;
          top: 0;
          right: 0;
          bottom: 0;
          left: 0;
        }
        .background {
          img {
            width: 100%;
            height: 100%;
          }
        }
        .message {
          padding: 20px;
          .inline-block {
            display: inline-block;
            vertical-align: middle;
          }
          .height-100 {
            height: 100%;
          }
          .text {
            margin-bottom: 20px;
            font-size: 24px;
            font-weight: bold;
            color: #d08490;
          }
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
    }
  }
}

@keyframes fall {
  from {
    top: -220px;
  }
  to {
    top: 200px;
  }
}
</style>
