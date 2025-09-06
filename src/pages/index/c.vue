<template>
	<view>
		<view class="container">
			<view class="circle" @click="toggleSidebar">
				<image class="circle-img" src="/static/a.jpg"></image>
			</view>
			<view class="search-box">
                <input class="search-input" type="text" v-model="searchValue" placeholder="请输入关键词..." />
                <button class="search-btn" @click="handleSearch">搜索</button>
            </view>
		</view>
		<view class="black-line"></view>
        <scroll-view class="scroll-container" scroll-x="true">
            <view class="scroll-content">
                <view class="card" v-for="(item, index) in 5" :key="index">
                    <text class="card-text">项目 {{ index + 1 }}</text>
                </view>
            </view>
        </scroll-view>
        <view class="black-line"></view>
        <view class="empty-space"></view>
        <view class="center-box">
            <text class="box-text">推荐项目1</text>
        </view>
        <view class="empty-space"></view>
        <view class="center-box">
            <text class="box-text">推荐项目2</text>
        </view>
        <view class="empty-space"></view>
        <view class="center-box">
            <text class="box-text">推荐项目3</text>
        </view>
        <view class="black-line"></view>
        <view class="circle-container">
            <!-- 左侧圆圈 -->
            <view class="circle"></view>

            <!-- 中间的带 "+" 号的圆圈 -->
            <view class="circle plus-circle">+</view>

            <!-- 右侧圆圈 -->
            <view class="circle"></view>
        </view>
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
  border: 4rpx solid #87cefa; /* 淡黄色背景 */
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

.search-box {
  display: flex;
  padding: 10rpx;
  border: 1px solid #ccc;
  border-radius: 10rpx;
  height: 50rpx;
  width:300px;
}

.search-input {
  flex: 1;
  padding: 10rpx;
  border: none;
}

.search-btn {
  padding: 10rpx;
  background-color: #007aff;
  color: white;
  border: none;
  border-radius: 5rpx;
  height: 50rpx;
  line-height: 40rpx;
  font-size: 24rpx; /* 调小文字大小 */
}

.black-line {
  width: 100%;
  height: 4rpx;
  background-color: black;
  margin: 20rpx 0;
  display: block;
}

.scroll-container {
  width: 100%;
  overflow: auto;
  white-space: nowrap; /* 让子元素不换行，支持横向滚动 */
}

.scroll-content {
  display: flex; /* 让卡片横向排列 */
}

.card {
  width: 200rpx;
  height: 150rpx;
  background-color: #f0f8ff;
  border: 2rpx solid #87cefa;
  border-radius: 20rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 20rpx;
  flex-shrink: 0; /* 防止卡片被压缩 */
}

.center-box {
  width: 700rpx; /* 控制矩形的宽度 */
  height: 200rpx; /* 控制矩形的高度 */
  border: 4rpx solid #87CEFA; /* 设置淡蓝色边框 */
  display: flex; /* 让里面的文字居中 */
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
  margin: 0 auto; /* 水平居中 */
  background-color: #FFFACD; /* 可选背景色 */
  border-radius: 20rpx;
}

.box-text {
  font-size: 32rpx;
  color: #333;
}

.empty-space {
  height: 20rpx; /* 控制空行的高度 */
}

.circle-container {
  display: flex;
  justify-content: space-between; /* 让三个圆圈等间距排列 */
  align-items: center;
  width: 80%; /* 让它不占满全屏，左右留点空间 */
  margin: 50rpx auto; /* 居中 */
}

/* 中间的带 "+" 的圆圈 */
.plus-circle {
  font-size: 48rpx;
  font-weight: bold;
  color: black;
  border: 4rpx solid #87CEFA;
}

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
