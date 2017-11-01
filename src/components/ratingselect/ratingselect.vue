<template>
	<div class="ratingselect">
	  <div class="rating-type border-1px">
	  	<span @click="select(2,$event)" class="block positive" :class="{'active':selectTypeNum===2}">{{desc.all}}<span class="count">40</span></span>
	  	<span  @click="select(0,$event)" class="block positive" :class="{'active':selectTypeNum===0}">{{desc.positive}}<span class="count">56</span></span>
	  	<span  @click="select(1,$event)" class="block negative" :class="{'active':selectTypeNum===1}">{{desc.negative}}<span class="count">9</span></span>
	  </div>
	  <div class="switch" :class="{'on':onlyCont}" @click="toggleContent">
	  	<span class="icon-check_circle"></span>
	  	<span class="text">只看有内容的评价</span>
	  </div>
	</div>
</template>

<script type="text/ecmascript-6">
  // const POSITIVE = 0;
  // const NEGATIVE = 1;
  const ALL = 2;
  export default {
    props: {
      ratings: {
        type: Array,
        default () {
          return [];
        }
      },
      selectType: {
        type: Number,
        default: ALL
      },
      onlyContent: {
        type: Boolean,
        default: false
      },
      desc: {
        type: Object,
        default () {
          return {
            all: '全部',
            positive: '满意',
            nagetive: '不满意'
          };
        }
      }
    },
    data () {
      return {
        selectTypeNum: this.selectType,
        onlyCont: this.onlyContent
      };
    },
    watch: {
      selectType (val) {
        this.selectTypeNum = val;
      },
      onlyContent (val) {
        this.onlyCont = val;
      }
    },
    methods: {
      select (type, event) {
        if (!event._constructed) {
          return;
        }
        this.selectTypeNum = type;
        this.$emit('selectType', type);
      },
      toggleContent (event) {
        if (!event._constructed) {
          return;
        }
        this.onlyCont = !this.onlyCont;
        this.$emit('onlyContent', this.onlyCont);
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixim";  
  .rating
      padding-top 18px
      .title
        line-height 14px
        margin-left 18px
        font-size 14px
        color rgb(7,17,27)
    .ratingselect
      .rating-type
        padding 18px 0
        margin 0 18px
        border-1px(rgba(7,17,27,0.1))
        font-size 0
        .block
          display inline-block
          padding 8px 12px
          margin-right 8px
          border-radius 1px
          font-size 12px
          line-height 16px
          color rgb(77,85,93)
          &.active
            color #fff
          .count
            margin-left 2px
            font-size 8px
          &.positive
            background rgba(0,160,220,0.2)
            &.active
              background rgb(0,160,220)
          &.negative
            background rgba(77,85,93,0.2)
            &.active
              background rgb(77,85,93)
      .switch
        padding 12px 18px
        line-height 24px
        border-bottom 1px solid rgba(7,17,27,0.1)
        color rgb(147,153,159)
        font-size 0
        &.on
          .icon-check_circle
            color #00c850
        .icon-check_circle
          margin-right 4px
          font-size 24px
        .text
          display inline-block
          vertical-align top
          font-size 12px
              
  
</style>