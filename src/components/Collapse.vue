<template>
  <div class="demo-collapse px-5">
    <el-collapse v-model="activeName" accordion>
      <el-collapse-item title="✨注意事项" name="1">
        <ol>
          <li>所有共享ID均来自网络收集</li>
          <li>不保证可用性</li>
        </ol>
      </el-collapse-item>
      <el-collapse-item title="✨注意事项" name="2">
        <ol>
          <li>禁止在设置中登录共享ID</li>
          <li>被锁概不负责</li>
        </ol>
      </el-collapse-item>
      <el-collapse-item title="✨注意事项" name="3">
        <ol>
          <li>下载完所需应用后请尽快退出</li>
          <li>
            <el-link type="primary" href="https://apps.apple.com/us/app/shadowrocket/id932747118?l=zh-Hans-CN">点我跳转到小火箭下载页</el-link>
          </li>
        </ol>
      </el-collapse-item>
      <el-collapse-item title="✨必看" name="4">
        <h3 class="place-content-center my-5" style=" color: red; text-align: center; font-size: 20px" >登录时的注意事项</h3>
        <div>
          <ImgInfo></ImgInfo>
        </div>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script lang="ts" setup>
import {ref} from 'vue'
import ImgInfo from "@/components/ImgInfo.vue";

const color = ref("green");
const activeName = ref('1')
</script>

