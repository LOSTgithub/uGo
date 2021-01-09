<template>
	<view class="home-container">
		<view class="search-box" :class="{focus: isFocus}">
      <input type="text" @focus="isFocus=true" @blur="isFocus=false" placeholder="搜索" />
      <icon type="search" size="20"></icon>
    </view>
    <swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
      <swiper-item v-for="(item, index) in swipers" :key="index">
        <view class="swiper-item">
          <image :src="item.image_src" mode="widthFix"></image>
        </view>
      </swiper-item>
    </swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isFocus: false, // 控制类名切换
        swipers: [] // 轮播图数据
			}
		},
		methods: {
			
		},
    onLoad () {
      uni.request({
        url: "https://www.uinav.com/api/public/v1/home/swiperdata",
        method: "get",
        success: (res) => {
          if(res.data.meta.status === 200) {
            this.swipers = res.data.message
          }
        }
      })
    }
	}
</script>

<style lang="less">
  .home-container {
    .search-box {
      background-color: #fe2c4b;
      padding: 20rpx;
      position: relative;
      input {
        backgrond-coolor: white;
        padding-left: 50%;
        border-radius: 10rpx;
        transition: .3s;
      }
      icon {
        position: absolute;
        top: 25rpx;
        left: 42%;
        transition: .3s;
      }
      &.focus {
        input {
          padding-left: 80rpx;
        }
        icon {
          left: 4%;
        }
      }
    }
  }
</style>
