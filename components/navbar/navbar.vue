<template>
	<view class="navbar">
		<view class="navbar-fixed">
      <!-- 状态栏 -->
      <view :style="{height: statusBarHeight + 'px'}"></view>
      <!-- 导航栏内容 -->
      <view class="navbar-content" :style="{height: navBarHeight + 'px', width: windowWidth + 'px'}">
        <view class="navbar-search">
          <view class="navbar-search_icon">
            <uni-icons type="search" size="16" color="#999"></uni-icons>
          </view>
          <view class="navbar-search_text">uni-app</view>
        </view>
      </view>
		</view>
    <view :style="{height: (statusBarHeight+navBarHeight) + 'px'}"></view>    
	</view>
</template>

<script>
	export default {
		data() {
			return {
				statusBarHeight: 20,
        navBarHeight: 45,
        windowWidth: 375
			};
		},
    created() {// 在实例创建完成后被立即调用
      // 同步获取手机系统信息
      const info  = uni.getSystemInfoSync();
      this.statusBarHeight = info.statusBarHeight;
      this.windowWidth = info.windowWidth;
      
      // #ifndef H5 || APP-PLUS || MP-ALIPAY
      // 获取胶囊的位置
      const menuButtonInfo =  uni.getMenuButtonBoundingClientRect();
      console.log(menuButtonInfo)
      
      // 导航栏高度=（胶囊底部高度-状态栏高度）+（胶囊顶部高度-状态栏高度）
      this.navBarHeight = (menuButtonInfo.bottom - info.statusBarHeight) + (menuButtonInfo.top - info.statusBarHeight);
      this.windowWidth = menuButtonInfo.left
      // #endif
    }
	}
</script>

<style lang="scss">
  .navbar {
    .navbar-fixed {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      z-index: 99;
      background-color: $mk-base-color;
      .navbar-content {
        display: flex;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        padding: 0 15px; 
        height: 45px;
        .navbar-search {
        display: flex;
        align-items: center;
        height: 30px;
        width: 100%;
        padding: 0 10px;
        background-color: #fff;
        border-radius: 30px;
        .navbar-search_icon {
          /* width: 10px;
          height: 10px;
          border: 1px red solid; */
          margin-right: 10px;
        }
        .navbar-search_text {
          font-size: 14px;
          color: #999;
        }
      }
      }
      
    }
  }
</style>
