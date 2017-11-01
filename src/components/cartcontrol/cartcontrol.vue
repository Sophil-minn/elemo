<template>
	<div class="cartcontrol">
	  <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart()">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>  
    <div class="cart-count"  v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart($event)"></div>
	</div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';

export default {
    props: {
      food: {
        type: Object
      }
    },
    created () {
      // console.log(this.food);
    },
    methods: {
      addCart (event) {
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
        this.$emit('increment', event.target);
        this.$emit('foodCom', event.target);
        return;
      },
      decreaseCart (event) {
        if (this.food.count) {
          this.food.count--;
        }
        return;
      }
    }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol-wrapper
    position absolute
    right 0
    bottom 12px
    height 30px
  .cartcontrol
    font-size 0
    .cart-decrease
      display inline-block
      font-size 24px
      transition all .4s linear
      .inner
        position relative
        display inline-block
        line-height 24px
        font-size 24px
        color rgb(0,160,220)
        transition all 0.4s linear
      &.move-transition
        opacity 1
        transform translate3D(0, 0, 0)
        .inner
          position relative
          transform: rotate(0)
      &.move-enter
        opacity 0 
        transform: translate3D(24px,0,0)
        .inner
          position absolute
          transform: rotate(180deg)
      &.move-leave-active
        opacity 0 
        transform: translate3D(24px,0,0)
        .inner
          position absolute
          left -24px
          top -24px
          transform: rotate(180deg)
    .cart-count
      display inline-block
      font-size 10px
      vertical-align top
      width 12px
      padding-top 6px
      line-height 24px
      text-align center
      color rgb(147,153,159)
    .cart-add
      display inline-block
      padding-top 6px
      line-height 24px
      font-size 24px
      color rgb(0,160,220)
</style>