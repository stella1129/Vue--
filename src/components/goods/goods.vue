<template>
  <div class="goods">
	<div class="menu-wrapper">
		<ul>
			<li v-for="item in goods" class="menu-item">
				<span class="text border-1px">
				    <span v-show="item.type > 0" class="icon" :class="classMap[item.type]">
				    </span>
				    {{item.name}}
				</span>
			</li>
		</ul>
	</div>
	<div class="foods-wrapper">
		<ul>
			<li v-for="item in goods" class="food-list">
				<h1 class="title">{{item.name}}</h1>
				<ul>
					<li v-for="food in item.foods" class="food-item border-1px">
						<div>
							<img :src="food.icon" width="57" height="57" class="icon">
						</div>
						<div class="content">
							<h2 class="name">{{food.name}}</h2>
							<p class="desc" v-show="food.description">{{food.description}}</p>
							<div class="extra">
								<span class="count">月售{{food.sellCount}}份</span>
								<span>好评率{{food.rating}}%</span>
							</div>
							<div class="price">
								<span class="now">￥{{food.price}}</span>
								<span v-show="food.oldPrice" class="old">￥{{food.oldPrice}}</span>
							</div>
						</div>
					</li>
				</ul>
			</li>
		</ul>
	</div>
  </div>
</template>

<script>
  const ERR_OK = 0;
  export default{
    props: {
        seller: {
            type: Object
        }
    },
    data () {
        return {
           goods: []
        };
    },
    created () {
        this.$http.get('/api/goods').then((response) => {
            response = response.body;
            console.log(response);
            if (response.errno === ERR_OK) {
                this.goods = response.data;
                console.log(this.goods);
            };
        });
        this.classMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
    }
  };
</script>

<style lang="stylus" rel="stylesheets/stylus">
  @import "../../common/stylus/mixin";

.goods
  display: flex
  position:absolute
  width: 100%
  top: 174px
  bottom: 46px
  overflow: hidden
  .menu-wrapper
    flex: 0 0 80px
    width:80px
    background: #f3f5f7
    .menu-item
      display:table
      height: 54px
      width: 56px
      line-height: 14px
      padding:0 12px
      .icon
        display:inline-block
        width: 12px
        height: 12px
        margin-right: 2px
        background-size: 12px
        background-repeat: no-repeat
        &.decrease
          bg-img('decrease_3')
        &.discount
          bg-img('discount_3')
        &.guarantee
          bg-img('guarantee_3')
        &.invoice
          bg-img('invoice_3')
        &.special
          bg-img('special_3')
      .text
        display:table-cell
        vertical-align: middle
        border-1px(rgba(7,17,27,0.1))
        font-size: 12px
        font-weight: 200
  .foods-wrapper
    flex: 1
    .title
      padding-left:14px
      font-size: 12px
      color: rgb(147,153,159)
      height:26px
      line-height:26px
      border-left: #d9dde1 solid 2px
      background: #f2f5f7
    .food-item
      display: flex
      margin: 18px
      padding-bottom: 18px
      border-1px(rgba(7,17,27,0.1))
      &:last-child
        border-none()
        margin-bottom: 0
      .icon
        flex: 0 0 57px
        margin-right: 10px
      .content
        flex:1
        .name
          margin:2px 0 8px 0
          height: 14px
          line-height: 14px
          font-size: 14px
          color: rgb(7,17,27)
        .desc, .extra
          font-size: 10px
          color: rgb(147,153,159)
          line-height: 10px
        .desc
          margin: 8px 0 8px 0
          line-height: 12px
        .extra  
          .count
            margin-right: 12px
        .price
          font-weight: 700
          line-height: 24px
          .now
            font-size: 14px
            color:rgb(240,20,20)
            margin-right: 8px
          .old
            font-size: 10px
            color:rgb(147,153,159)
            text-decoration: line-through

            





      



  

	
</style>