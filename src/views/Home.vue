<template>
  <div class="home">
    <div class="content">
      <div class="start">
        <img src="../assets/images/page_1.jpg">
      </div>
      <div class="picture-container">
        <div class="picture">
          <img src="../assets/images/picture.jpg">
        </div>
        <img src="../assets/images/page_2.jpg">
      </div>
      <div class="end">
        <img src="../assets/images/page_3.jpg">
      </div>
      <InvitationForm></InvitationForm>
    </div>
    <div class="cover">
      <div class="middle"></div>
      <img src="../assets/images/cover.jpg">
    </div>
    <div class="sound" @click="sound()">
      <img src="../assets/images/sound.svg">
      <div class="close"></div>
      <audio id="bgm" controls hidden :src="bgmUrl" @canplay="play()"></audio>
    </div>
  </div>
</template>

<script>
import InvitationForm from '../components/InvitationForm.vue';

export default {
  name: 'home',
  components: { InvitationForm },
  data: () => ({ bgmUrl: '' }),
  methods: {
    animation() {
      const cover = document.getElementsByClassName('cover')[0];
      const content = document.getElementsByClassName('content')[0];
      this.fade(cover, content, 1);
    },
    fade(cover, content, opacity) {
      cover.style.opacity = opacity;
      content.style.opacity = 1 - opacity;
      if (opacity > 0) {
        setTimeout(() => {
          this.fade(cover, content, opacity - 0.05);
          window.scrollTo({ left: 0, top: 0 });
        }, 60);
      } else {
        setTimeout(() => {
          document.body.style.overflow = 'auto';
          document.getElementById('invitation-form-container').style.display = 'block';
        }, 120);
      }
    },
    sound() {
      const sound = document.getElementsByClassName('close')[0];
      if (sound.style.display === 'block') {
        sound.style.display = 'none';
        document.getElementById('bgm').play();
      } else {
        sound.style.display = 'block';
        document.getElementById('bgm').pause();
      }
    },
    play() {
      const playPromise = document.getElementById('bgm').play();
      playPromise
        .then(() => {})
        .catch(error => {
          console.log(error);
          this.sound();
        });
    },
    getBgmUrl() {
      if (
        window.location.host.indexOf('localhost') > -1 ||
        window.location.host.indexOf('192.168.0.103') > -1
      ) {
        this.bgmUrl = 'https://192.168.0.103:8080/wedding/bgm.mp3';
      } else {
        this.bgmUrl = 'https://www.calicomoo.ml:8080/wedding/bgm.mp3';
      }
    }
  },
  created() {
    this.getBgmUrl();
  },
  mounted() {
    setTimeout(() => {
      this.animation();
    }, 1500);
  }
};
</script>

<style lang="scss" scoped>
.content {
  .start {
    margin: 10px 0 0 10px;
  }
  .picture-container {
    display: inline-block;
    position: relative;
    width: 1200px;
    max-width: 100%;
    .picture {
      position: absolute;
      top: 6%;
      right: 12%;
      left: 12%;
    }
  }
  img {
    display: inline-block;
    max-width: 100%;
  }
  .end {
    img {
      max-width: 40%;
    }
  }
}
.sound {
  position: fixed;
  top: 0;
  right: 2px;
  opacity: 0.8;
  cursor: pointer;
  z-index: 9999;
  img {
    width: 30px;
    height: 30px;
  }
  .close {
    display: none;
    border-top: 2px solid #888888;
    border-bottom: 2px solid #888888;
    border-radius: 2px;
    position: fixed;
    top: 13px;
    right: 0;
    width: 35px;
    transform: rotate(315deg);
  }
}
.cover {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: #d08490;
  .middle {
    display: inline-block;
    height: 100%;
    vertical-align: middle;
  }
  img {
    display: inline-block;
    max-width: 100%;
    vertical-align: middle;
  }
}
</style>
