<template>
	<view>
		<view class="container">
			<view class="circle" @click="toggleSidebar">
				<image class="circle-img" src="/static/a.jpg"></image>
			</view>
			<text class="text">人生苦短, 我用python</text>
		</view>
		<view class="black-line"></view>
		<view class="third-row">
			<text class="word first-word">足迹</text>
			<text class="word second-word">收藏</text>
		</view>
		<view class="black-line"></view>
		<view>
			<text class="text">我的帖子</text>
		</view>
		<view class="black-line"></view>
		<view>
			<text class="text">意见反馈</text>
		</view>
		<view class="black-line"></view>
		<view>
			<text class="text">联系我们</text>
		</view>
		<view class="black-line"></view>
    <!-- 遮罩层，点击后关闭侧边栏 -->
    <view v-if="sidebarVisible" class="overlay" @click="toggleSidebar"></view>

    <!-- 侧边栏 -->
    <view :class="{'sidebar-visible': sidebarVisible}" class="sidebar-content">
      <text class="close-btn" @click="toggleSidebar">×</text>

      <!-- 用户信息 -->
      <view class="user-info">
        <image src="/static/a.jpg" class="avatar"></image>
        <text class="username">{{ username }}</text>
      </view>

      <!-- 菜单项 -->
      <view class="menu-item" @click="goToPage('/pages/index/d')">我的帖子</view>
      <view class="menu-item" @click="goToPage('/pages/orders')">我的收藏</view>
      <view class="menu-item" @click="goToPage('/pages/profile')">我的消息</view>
      <view class="menu-item" @click="goToPage('/pages/settings')">意见反馈</view>
      <view class="menu-item" @click="goToPage('/pages/settings')">联系我们</view>
      <view class="menu-item" @click="logout">退出登录</view>
    </view>




	</view>

</template>

<style>
/* 侧边栏样式 */
.sidebar-content {
  position: fixed;
  top: 0;
  left: 0;
  width: 60%;
  height: 100vh;
  background-color: #FFFACD;
  box-shadow: -5rpx 0 20rpx rgba(0, 0, 0, 0.2);
  z-index: 1001;
  padding: 20rpx;
  transition: transform 0.3s ease-in-out;
  display: flex;
  flex-direction: column;
    /* 让侧边栏默认隐藏在左边 */
  transform: translateX(-100%);
  transition: transform 0.3s ease-in-out;
}

/* 当 sidebarVisible 为 true 时，侧边栏滑出 */
.sidebar-visible {
  transform: translateX(0);
}


/* 遮罩层 */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  z-index: 1000;
}

/* 关闭按钮 */
.close-btn {
  font-size: 40rpx;
  text-align: right;
  padding: 10rpx;
  cursor: pointer;
}

/* 用户信息 */
.user-info {
  display: flex;
  align-items: center;
  padding: 20rpx;
}

.avatar {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  margin-right: 20rpx;
}

.username {
  font-size: 36rpx;
  color: #333;
}

/* 菜单项 */
.menu-item {
  padding: 20rpx;
  font-size: 32rpx;
  color: #333;
  border-bottom: 1rpx solid #ccc;
}
.menu-item:hover {
  background-color: #FFFACD;
}

.btn-container {
  display: flex;  /* 使用Flex布局 */
  justify-content: space-around; /* 让按钮均匀分布 */
  padding: 20rpx;
}

.btn {
  padding: 20rpx 40rpx;
  font-size: 32rpx;
  color: white;
  background-color: #87cefa;
  border: none;
  border-radius: 20rpx;
}

.container {
  display: flex; /* 让图片和文字水平排列 */
  align-items: center; /* 垂直居中对齐 */
  padding: 20rpx;
}

.circle {
  width: 100rpx;
  height: 100rpx;
  border-radius: 50%;
  overflow: hidden;
  background-color: #f0e68c; /* 淡黄色背景 */
  display: flex;
  align-items: center;
  justify-content: center;
}

.circle-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.text {
  margin-left: 20rpx; /* 文字和图片之间的间距 */
  font-size: 32rpx;
  color: #333;
}

.black-line {
  width: 100%;
  height: 4rpx;
  background-color: black;
  margin: 20rpx 0;
  display: block;
}
/* 第三行：两个词排布 */
.third-row {
  display: flex;
  justify-content: space-between; /* 让两个词均匀分布 */
  padding: 0 10%; /* 给左右两侧留点空间 */
}

/* 两个词的样式 */
.word {
  font-size: 28rpx;
  color: #555;
  margin-top: 40rpx;  /* 增加上方间距 */
  margin-bottom: 40rpx; /* 增加下方间距 */
}

/* 让第一个词靠近 1/3 处 */
.first-word {
  margin-left: 10%;
}

/* 让第二个词靠近 2/3 处 */
.second-word {
  margin-right: 10%;
}

</style>

<script>
export default {
  data() {
    return {
      searchValue: "",
      username: "高飞",
      sidebarVisible: false // 控制侧边栏显示/隐藏
    };
  },
  methods: {
    handleSearch() {
      uni.showToast({
        title: "搜索：" + this.searchValue,
        icon: "none"
      });
    },
    goToPage(url) {
      uni.navigateTo({
        url: url
      });
    },
    toggleSidebar() {
      this.sidebarVisible = !this.sidebarVisible;
    },
    logout() {
      uni.showToast({
        title: "退出登录",
        icon: "none"
      });
    }
  }
};

</script>
