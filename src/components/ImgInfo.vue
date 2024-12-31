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
        {'url': 'src/img/img1.jpg', 'title': `点击'右上角头像'`},
        {'url': 'src/img/img2.jpg', 'title': `点击'退出登录'`},
        {'url': 'src/img/img3.jpg', 'title': `点击'通过Apple账户登录'`},
        {'url': 'src/img/img4.jpg', 'title': `输入复制的账号密码`},
        {'url': 'src/img/img5.jpg', 'title': `点击'其他选项'`},
        {'url': 'src/img/img6.jpg', 'title': `点击'不升级'`}
    ]
const srcList = [
  'src/img/img1.jpg',
  'src/img/img2.jpg',
  'src/img/img3.jpg',
  'src/img/img4.jpg',
  'src/img/img5.jpg',
  'src/img/img6.jpg',
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