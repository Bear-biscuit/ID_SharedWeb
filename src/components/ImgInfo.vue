<template>
    <div class="demo-image flex flex-row flex-wrap">
      <div v-for="(item,index) in urlList" :key="index" class="block basis-1/2">
        <span class="demonstration">{{ item.title }}</span>
        <el-image :preview-src-list="srcList" style="width: 50%" :src="item.url"/>
      </div>
    </div>
</template>

<script lang="ts" setup>
const urlList =[
        {'url': 'public/img/img1.jpg', 'title': `点击'右上角头像'`},
        {'url': 'public/img/img2.jpg', 'title': `点击'退出登录'`},
        {'url': 'public/img/img3.jpg', 'title': `点击'通过Apple账户登录'`},
        {'url': 'public/img/img4.jpg', 'title': `输入复制的账号密码`},
        {'url': 'public/img/img5.jpg', 'title': `点击'其他选项'`},
        {'url': 'public/img/img6.jpg', 'title': `点击'不升级'`}
    ]
const srcList = [
  'public/img/img1.jpg',
  'public/img/img2.jpg',
  'public/img/img3.jpg',
  'public/img/img4.jpg',
  'public/img/img5.jpg',
  'public/img/img6.jpg',
]
</script>

<style scoped>
.demo-image .block {
  padding: 30px 0;
  text-align: center;
  border-right: solid 1px var(--el-border-color);
  display: inline-block;
  box-sizing: border-box;
  vertical-align: top;
}

.demo-image .block:last-child {
  border-right: none;
}

.demo-image .demonstration {
  display: block;
  color: #396bec;
  font-size: 14px;
  margin-bottom: 20px;
}
</style>
