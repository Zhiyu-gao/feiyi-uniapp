<template>
    <view>
      <view class="container">
        <text class="text">项目名称：{{ project.name }}</text>
      </view>
      <view>
        <image :src="project.img" mode="widthFix" style="width: 200px; height: 200px;"></image>
      </view>
      <view class="black-line"></view>
      <view class="container">
        <text class="text">项目内容：{{ project.content }}</text>
      </view>
      <view class="black-line2"></view>
      <view class="container">
        <text class="text">传承人：{{ project.owner }}</text>
      </view>
    </view>
  </template>

<script>
export default {
  data() {
    return {
      project: {
        name: '',
        img: '',
        content: '',
        owner: ''
      }
    };
  },
  onLoad(option) {
    if (option.results) {
      const results = JSON.parse(decodeURIComponent(option.results));
      // 假设只显示第一个搜索结果
      if (results.length > 0) {
        this.project.name = results[0].name;
        this.project.img = results[0].img; // 确保是可访问的 URL
        this.project.content = results[0].content;
        this.project.owner = results[0].owner;
      }
    }
  }
};
</script>

  
  
<style>
.container {
padding: 20rpx;
}

.text {
font-size: 28rpx;
color: #333;
}

.black-line {
width: 100%;
height: 4rpx;
background-color: black;
margin: 20rpx 0;
display: block;
}

.black-line2 {
width: 100%;
height: 4rpx;
background-color: black;
margin: 20rpx 0;
display: block;
margin-top: 400px; /* 设置线条上方的间距 */
}
</style>
  