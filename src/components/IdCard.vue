<template>
  <div  class="bg-white shadow-sm rounded-md p-3 h-40 flex flex-col justify-between">
    <div>
      <div class="flex justify-between items-center mb-2">
        <h2 class="text-sm font-semibold text-gray-800">Shadowrocket</h2>
        <span class="text-xs px-2 py-0.5  text-green-800 rounded"
        :class="{
          'bg-green-100':availability==='正常',
          'bg-red-100':availability!=='正常',
        }">{{availability}}</span>
      </div>
      <div class="mb-2">
        <p class="text-xs text-gray-600 truncate">账号: {{account}}</p>
        <p class="text-xs text-gray-600">密码: ******</p>
      </div>
    </div>
    <div class="flex space-x-2">
      <button class="flex-1 bg-blue-400 text-white py-1 rounded text-xs hover:bg-blue-500 transition"
              @click="copyText(account)">
        复制账号
      </button>
      <button class="flex-1 bg-green-400 text-white py-1 rounded text-xs hover:bg-green-500 transition"
              @click="copyText(password.replace(/\\u([\dA-Fa-f]{4})/g, (_, code) =>
                                String.fromCharCode(parseInt(code, 16))
                        ))">
        复制密码
      </button>
    </div>
  </div>
</template>

<script>
import {ElMessage, ElNotification} from "element-plus";
export default {
  data(){
    return{
    isShow:false
    }
  },
  props:{
    availability: String,
    account:String,
    password: String,
  },
  methods: {
    copyText(text) {
      try {
        navigator.clipboard.writeText(text);
        this.openS()
      } catch (err) {
        console.error('复制出错', err);
        this.openE()
      }
    },
    openS(){
      ElNotification({
        title: 'Success',
        message: '复制成功',
        type: 'success',
        duration: 2000,
      })
    },
    openE(){
      ElNotification({
        title: 'Error',
        message: '复制失败',
        type: 'error',
        duration: 2000,
      })
    }
  }
}
</script>