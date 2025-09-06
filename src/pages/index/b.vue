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
    <view class="center-text">全部项目</view>
    <view class="empty-space"></view>
    <view class="center-box" @click="goToPage('/pages/index/d')">
      <text class="box-text">项目1</text>
    </view>
    <view class="empty-space"></view>
    <view class="center-box">
      <text class="box-text">项目2</text>
    </view>
    <view class="empty-space"></view>
    <view class="center-box">
      <text class="box-text">项目3</text>
    </view>
    <view class="empty-space"></view>
    <view class="center-box">
      <text class="box-text">项目4</text>
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

.center-text {
  text-align: center; /* 水平居中 */
  font-size: 32rpx;
  color: #333;
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
      const keyword = this.searchValue.trim();
      if (!keyword) {
        uni.showToast({ title: '请输入关键词', icon: 'none' });
        return;
      }

      uni.request({
        url: `http://127.0.0.1:8000/api/projects/?name=${encodeURIComponent(keyword)}`,  // 注意替换成你的后端地址
        method: 'GET',
        success: (res) => {
          const results = res.data;
          if (results.length > 0) {
            // 成功：跳转到 d.vue，并携带项目数据
            uni.navigateTo({
              url: `/pages/index/d?results=${encodeURIComponent(JSON.stringify(results))}`
            });
          } else {
            // 没找到
            uni.showToast({ title: '未找到项目', icon: 'none' });
          }
        },
        fail: () => {
          uni.showToast({ title: '请求失败', icon: 'none' });
        }
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
