<template lang="pug">
    div#clock
        div#lines
            for val in [1,2,3,4]
                div.line
        div#numbers
            for val in [3,6,9,12]
                div=val
        div#pointers
            div#hour(v-bind:style="{transform:'rotate('+h+'deg)'}")
            div#min(v-bind:style="{transform:'rotate('+m+'deg)'}")
            div#sec(v-bind:style="{transform:'rotate('+s+'deg)'}")
</template>

<style lang="less">
@borderColor: #1e90ff;
@contentColor: #70a1ff;
#clock {
  height: 400px;
  width: 400px;
  background: @contentColor;
  border-radius: 50%;
  border: 20px solid @borderColor;
  box-shadow: 0 20px 20px gray, inset 0 0 10px @borderColor;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  #lines {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    width: 100%;
    height: 100%;
    &::after {
      content: "";
      position: absolute;
      background: @contentColor;
      z-index: 6;
      width: 90%;
      height: 90%;
      border-radius: 50%;
    }
    .line {
      width: 8px;
      height: 100%;
      background: #000;
      z-index: 5;
      position: absolute;
      &:nth-child(1) {
        transform: rotate(30deg);
      }
      &:nth-child(2) {
        transform: rotate(60deg);
      }
      &:nth-child(3) {
        transform: rotate(120deg);
      }
      &:nth-child(4) {
        transform: rotate(150deg);
      }
    }
  }
  #numbers {
    height: 100%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    div {
      z-index: 7;
      font-size: 5em;
      position: absolute;
      margin: 0;
      padding: 0;
      line-height: 1em;
      &:nth-child(1) {
        right: 0;
      }
      &:nth-child(2) {
        bottom: 0;
      }
      &:nth-child(3) {
        left: 0;
      }
      &:nth-child(4) {
        top: 0;
      }
    }
  }
  #pointers {
    width: 100%;
    height: 100%;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    #hour {
      z-index: 8;
      width: 10px;
      height: 20%;
      background: #000;
      position: absolute;
      top: 30%;
      border-radius: 5px 5px 0 0;
      transform-origin:center bottom;
    //   transform: rotate(30deg);
    }
    #min {
      z-index: 8;
      width: 6px;
      height: 30%;
      background: #000;
      position: absolute;
      top: 20%;
      border-radius: 3px 3px 0 0;
      transform-origin:center bottom;
    //   transform: rotate(60deg);
    }
    #sec {
      z-index: 8;
      width: 4px;
      height: 50%;
      background: red;
      position: absolute;
      top: 10%;
      border-radius: 2px 2px 0 0;
      transform-origin: 50% 80%;
    //   transform: rotate(90deg);
    }
  }
  &::after {
    content: "";
    width: 20px;
    height: 20px;
    background: #000;
    position: absolute;
    z-index: 10;
    border-radius: 50%;
    border: solid 3px white;
    box-shadow: 0 0 10px white;
  }
}
</style>

<script>
export default {
    data:function(){
        return {
            h:0,
            m:0,
            s:0
        }
    },
    mounted:function(){
        setInterval(function(){
            let day = new Date();
            this.h=(day.getHours()+day.getMinutes()/60)*30;
            this.m=day.getMinutes()*6;
            this.s=day.getSeconds()*6;
        }.bind(this),1000)
    }
}
</script>