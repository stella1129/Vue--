<template>
	<div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img width="64" height="64" :src="seller.avatar">
			</div>
			<div class="content">
				<div class="title">
				    <span class="brand"></span>
				    <span class="name">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<!-- v-if 因为seller本来是个空的，数据获取是异步的，一开始为空，会出错-->
				<div v-if="seller.supports" class="supports">
					<span class="icon" v-bind:class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{seller.supports[0].description}}</span> 
				</div>
      </div>
      <div v-if="seller.supports" class="support-count" v-on:click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
		</div>
		<div class="bulletin-wrapper" v-on:click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div class="detail" v-show="detailShow">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <star :size="48" :score="seller.score"></star>
        </div>
      </div>
      <div class="detail-close">
        <i class="icon-close"></i>
      </div>
    </div>
	</div>
</template>

<script type="text/ecmascript-6">
  import star from 'components/star/star.vue';
  
  export default{
    props: {
      seller: {
        type: Object
      }
    },
    components: {
      star
    },
    data () {
      return {
        detailShow: false
      };
    },
    created () {
      this.classMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
    },
    methods: {
      showDetail: function () {
        this.detailShow = true;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin";

  .header
    position: relative
    overflow: hidden
    color: #fff
    background: rgba(7, 17, 27, 0.5)
    .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avatar
        display: inline-block
        img
          border-radius: 2px
      .content
        vertical-align:top
        display: inline-block
        margin-left: 16px
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            bg-img('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-size: 16px
            font-weight: bold
            line-height: 18px
        .description
          margin-bottom: 10px
          font-size: 12px
          line-height: 12px
        .supports
          .icon
            display:inline-block
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px
            background-repeat: no-repeat
            &.decrease
              bg-img('decrease_1')
            &.discount
              bg-img('discount_1')
            &.guarantee
              bg-img('guarantee_1')
            &.invoice
              bg-img('invoice_1')
            &.special
              bg-img('special_1')
          .text
            vertical-align:top
            font-size: 10px
            line-height: 12px
      .support-count
        position: absolute
        right: 12px
        bottom: 14px
        padding: 0 8px
        height: 24px
        line-height: 24px
        border-radius: 14px
        background: rgba(0, 0, 0, 0.2)
        text-align: center
        .count
          vertical-align:top
          font-size: 10px
        .icon-keyboard_arrow_right
          font-size: 10px
          line-height: 24px
          margin-left:2px
    .bulletin-wrapper
      position: relative
      height: 28px
      line-height:28px
      padding: 0 22px 0 12px
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      background: rgba(7, 17, 27, 0.2)
      .bulletin-title
        vertical-align:top
        display:inline-block
        margin-top: 8px
        width: 22px
        height: 12px
        bg-img('bulletin')
        background-size: 22px 12px
        background-repeat: no-repeat
      .bulletin-text
        vertical-align:top
        margin: 0 4px
        font-size: 10px
        line-height: 28px
      .icon-keyboard_arrow_right
        position: absolute
        font-size: 10px
        right: 12px
        top: 8px
    .background
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)
    .detail
      position: fixed
      z-index: 100
      top: 0 
      left: 0
      width: 100%
      height: 100%
      overflow: auto
      background: rgba(7, 17, 27, 0.8)
      .detail-wrapper
        min-height:100%
        width: 100%
        .detail-main
          margin-top: 64px
          padding-bottom: 64px
          .name
            font-size: 16px
            line-height: 16px
            font-weight: 700
            text-align: center
      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        font-size: 32px
        
























        





	
</style>