<template>
	<div class="ratings" ref="ratings">
		<div class="ratings-content">
			<div class="overview">
				<div class="overview-left">
					<h1 class="score">{{seller.score}}</h1>
					<div class="title">综合评分</div>
					<div class="rank">高于周边商家{{seller.rankRate}}</div>
				</div>
				<div class="overview-right">
					<div class="score-wrapper">
						<div class="title">服务态度</div>
						<star :size="36" :score="seller.serviceScore"></star>
						<span class="score">{{seller.serviceScore}}</span>
					</div>
					<div class="score-wrapper">
						<div class="title">商品评分</div>
						<star :size="36" :score="seller.serviceScore"></star>
						<span class="score">{{seller.foodScore}}</span>
					</div>
					<div class="delivery-wrapper">
						<span class="title">送达时间</span>
						<span class="delivery">{{seller.deliveryTime | formatDate}}分钟</span>
					</div>
				</div>
			</div>
  		<split></split>
  		<ratingselect @selectType="selectTypeChild" @onlyContent="onlyContentChild" :select-type="selectType" :only-content="onlyContent" :ratings="ratings"></ratingselect>
      <div class="rating-wrapper">
        <ul>
          <li v-for="rating in ratings" class="rate-item" v-show="needShow(rating.rateType, rating.text)">
            <div class="avatar">
              <img :src="rating.avatar" width="28" height="28">
            </div>
            <div class="content">
              <h1 class="name">{{rating.username}}</h1>
              <div class="star-wrapper">
                <star :size="24" :score="ratings.score"></star>
                <span class="delivery">
                  {{rating.deliveryTime}}
                </span>
              </div>
              <p class="text">{{rating.text}}</p>
              <div class="recommend">
                <span class="icon-thumb_up"></span>
                <span v-for="item in rating.recommend" class="item">{{item}}</span>
              </div>
              <div class="time">{{rating.rateTime | formatDate}}</div>
            </div>
          </li>
        </ul>
      </div>
  	</div>
  </div>
</template>

<script type="text/ecmascript-6">
import BScroll from 'better-scroll';
import {formatDate} from '../../common/js/date.js';
import star from '../../components/star/star';
import split from '../../components/split/split';
import ratingselect from '../../components/ratingselect/ratingselect';
// const ERR_OK = 0;
const ALL = 2;
export default{
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      ratings: [],
      selectType: ALL,
      onlyContent: true
    };
  },
  created () {
    // this.$http.get('/api/ratings').then((response) => {
    //   response = response.body;
    //   if (response.errno === ERR_OK) {
    //     this.ratings = response.data;
    //     this.$nextTick(() => {
    //       this.scroll = new BScroll(this.$refs['ratings'], {
    //         click: true
    //       });
    //     });
    //   }
    // });
    let appData = require('../../../data.json');
    this.ratings = appData.ratings;
    this.$nextTick(() => {
      this.scroll = new BScroll(this.$refs['ratings'], {
        click: true
      });
    });
  },
  filters: {
    formatDate (time) {
      let date = new Date(time);
      return formatDate(date, 'yyyy-MM-dd hh:mm');
    }
  },
  methods: {
    needShow (type, text) {
      if (this.onlyContent && !text) {
        return false;
      }
      if (this.selectType === ALL) {
        return true;
      } else {
        return type === this.selectType;
      }
    },
    selectTypeChild (type) {
      this.selectType = type;
      this.$nextTick(() => {
        this.scroll.refresh();
      });
    },
    onlyContentChild (onlyContent) {
      this.onlyContent = onlyContent;
      this.$nextTick(() => {
        this.scroll.refresh();
      });
    }
  },
  components: {
    star,
    split,
    ratingselect
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixim";
  @import "../../common/stylus/rating";  
  .ratings
  	position absolute
  	top 174px
  	bottom 0
  	left 0
  	width 100%
  	overflow hidden
  	.overview
  		display flex
  		padding 18px 0
  		.overview-left
  			flex 0 0 137px
  			padding 6px 0
  			width 137px
  			border-right 1px solid rgba(7, 17, 27, 0.1)
  			text-align center
  			.score
  				margin-bottom 6px
  				line-height 28px
  				font-size 24px
  				color rgb(255,153,0)
  			.title
  				margin-bottom 8px
  				line-height 12px
  				font-size 12px
  				color rgb(7,17,27)
  			.rank
  				line-height 10px
  				font-size 10px
  				color rgb(147,153,159)
  			@media only screen and (max-width: 320px) {
  				flex 0 0 120px
  				width 120px
  			}
  		.overview-right
  			flex 1
  			padding 6px 0 6px 24px
  			.score-wrapper
  				line-height 18px
  				margin-bottom 8px
  				font-size 0
  				.title
  					display inline-block
  					line-height 18px
  					font-size 12px
  					color rgb(7,17,27)
  				.star
  					display inline-block
  					vertical-align top
  					line-height 18px
  					margin 0 12px
  				.score
  					display inline-block
  					vertical-align top
  					line-height 18px
  					font-size 12px
  					color rgb(255,153,0)
  			.delivery-wrapper
  				font-size 0
  				.title
  					line-height 18px
  					font-size 12px
  					color rga(7,17,27)
  				.delivery
  					margin-left 12px
  					font-size 12px
  					color rgb(147,153,159)
  			@media only screen and (max-width: 320px) {
  				padding-left 6px
  			}   				  		
</style>

