<template>
  <div class="main-container">
    <div class="left">
      <div class="left-upper-text">
        Merry<br>Christmas
      </div>
      <div class="left-lower-text">
        Open your card
        <img :src="require('@/assets/spring.svg')" />
      </div>
    </div>
    <transition name="rp-fade-slide__right" appear mode="out-in">
      <div :key="artificialKey" @click="changeMessages" class="right" :class="{'no-after': message0 || message1}">
        <div v-if="!message0 && !message1">
            Click Me
        </div>
        <img v-if="message0 && !message1" :src="require(`@/assets/frame${sticker}a.gif`)" />
        <img v-if="!message0 && message1" :src="require(`@/assets/frame${sticker}b.png`)" />
      </div>
    </transition>
    <Snowf
      :amount="100"
      :size="8"
      :speed="2"
      :wind="1"
      :opacity="0.9"
      :swing="1"
      :image="null"
      :zIndex="null"
      :resize="true"
      color="#fff"
    />
  </div>
</template>

<script>
import Snowf from 'vue-snowf';
import { uuid } from 'vue-uuid';
export default {
  components: {
      Snowf
  },
  data(){
    return{
      message0: false,
      message1: false,
      artificialKey: uuid.v4(),
      messsage0Key: uuid.v4(),
      sticker: ''
    }
  },
  methods: {
    changeMessages(){
      if(!this.message0 &&  !this.message1){
        this.message0 = true;
      }
      else if(this.message0 && !this.message1){
        this.message0 = false;
        this.message1 = true;
      }
      else if(!this.message0 && this.message1){
        this.message0 = false;
        this.message1 = false;
      }
    }
  },
  watch: {
    message0(){
      this.artificialKey = uuid.v4();
    },
    message1(){
      this.artificialKey = uuid.v4();
    },
  },
  created(){
    let localSticker = localStorage.getItem("christmas-sticker")
    if(!localSticker){
      this.sticker = Math.floor((Math.random() * 7) + 1);
      localStorage.setItem("christmas-sticker", this.sticker)
    }
    else{
      this.sticker = localStorage.getItem("christmas-sticker");
    }
  }
};
</script>

<style lang="scss">
.main-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  gap: 200px;
  .left{
    height: auto;
    margin-top: 100px;
    .left-upper-text{
      font-size: 90px;
      font-family: 'Dancing Script', cursive;
      color: #fff;
      border-bottom: 6px solid #fff;
      padding-bottom: 28px;
      @media screen and (max-width: 920px) {
        font-size: 60px;
      }
      @media screen and (max-width: 800px) {
        text-align: center;
        border-bottom:  3px solid #fff;
      }
    }
    .left-lower-text{
      margin-top: 32px;
      font-size: 32px;
      font-weight: 500;
      color: #fff;
      display: flex;
      align-items: center;
      img{
        margin-left: 38px;
        @media screen and (max-width: 800px) {
          display: none;
        }
      }
      @media screen and (max-width: 920px) {
        font-size: 24px;
      }
      @media screen and (max-width: 800px) {
        text-align: center;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 15px;
      }
    }
    @media screen and (max-width: 800px) {
      background-color: rgba(0,0,0,0.6);
      padding: 20px;
      border-radius: 12px;
      width: 320px;
      margin-top: 50px;
    }
  }
  .right{
    z-index: 10000;
    width: 412px;
    height: 584px;
    position: relative;
    cursor: pointer;
    box-shadow: 0px 3.12121px 3.12121px rgba(0, 0, 0, 0.25);
    background-image: url('../assets/open.svg');
    font-style: normal;
    font-weight: 600;
    font-size: 46px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    font-family: 'Dancing Script', cursive;
    &::after{
      content: '';
      position: absolute;
      right: 0;
      height: 100%;
      background-color: #008269;
      width: 20px;
      box-shadow: inset 6px 4px 20px rgba(0, 0, 0, 0.4);
    }
    &.no-after::after{
      display:none;
    }
    img{
      @media screen and (max-width: 800px) {
        width: 350px;
      }
    }
    @media screen and (max-width: 800px) {
      margin-bottom: 50px;
      width: 350px;
      height: 496px;
    }
  }
  @media screen and (max-width: 1080px) {
    gap: 90px;
  }
  @media screen and (max-width: 920px) {
    gap: 20px;
  }
  @media screen and (max-width: 800px) {
    flex-direction: column;
  }
}
.rp-fade{
    &-enter-active, &-leave-active {
        transition: opacity .4s ease;
    }

    &-enter, &-leave-to{
        opacity: 0;
    }

    &-enter-to, &-leave {
        opacity: 1;
    }
}
.rp-fade-slide{
    &__up{
        &-enter-active, &-leave-active {
            transition: transform .2s ease, opacity .2s ease;
        }
        
        &-enter, &-leave-to{
            transform: translateY(16px);
            opacity: 0;
        }
        
        &-enter-to, &-leave {
            transform: translateY(0px);
            opacity: 1;
        }
    }

    &__down{
        &-enter-active, &-leave-active {
            transition: transform .2s ease, opacity .2s ease;
        }

        &-enter, &-leave-to{
            transform: translateY(-16px);
            opacity: 0;
        }

        &-enter-to, &-leave {
            transform: translateY(0px);
            opacity: 1;
        }
    }

    &__left{
        &-enter-active, &-leave-active {
            transition: transform .2s ease, opacity .2s ease;
        }

        &-enter, &-leave-to{
            transform: translateX(16px);
            opacity: 0;
        }

        &-enter-to, &-leave {
            transform: translateX(0px);
            opacity: 1;
        }
    }

    &__right{
        &-enter-active, &-leave-active {
            transition: transform .2s ease, opacity .2s ease;
        }

        &-enter, &-leave-to{
            transform: translateX(-16px);
            opacity: 0;
        }

        &-enter-to, &-leave {
            transform: translateX(0px);
            opacity: 1;
        }
    }
}
</style>
