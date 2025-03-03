<template>
  <el-dialog
      v-model="centerDialogVisible"
      title="注意事项"
      width="500"
      align-center
  >
    <div class="p-4 rounded-lg">
      <ul class="space-y-3">
        <li v-for="(item, index) in items" :key="index" class="flex items-center text-gray-700">
          <span class="mr-2 text-yellow-500">&#9733;</span>
          <span>{{ item }}</span>
        </li>
      </ul>
    </div>
    <template #footer>
      <div class="dialog-footer">
        <el-button type="primary" @click="centerDialogVisible = false">
          Ok
        </el-button>
      </div>
    </template>
  </el-dialog>
  <nav class="flex items-center justify-between w-full px-6 py-4 bg-white shadow-md">
    <div class="flex items-center space-x-4 w-full relative">
      <img
          src="../public/ShadowRocket.png"
          alt="Logo"
          class="h-10 w-auto"
      />
      <span class="text-xl font-bold text-gray-800">小火箭共享id</span>
      <img
          src="https://img.icons8.com/?size=100&id=62856&format=png&color=000000"
          alt="github"
          class="h-10 w-auto absolute right-0"
          @click="goToGitHub"
      >
    </div>
  </nav>
  <div class="mt-4">
    <Statistic
        :pv="pagePv"
        :uv="pageUv"></Statistic>
  </div>
  <div class="bg-gray-100 p-4">
    <el-scrollbar height="600px">
      <el-empty description="空" v-if="accounts.length===0"/>
      <div v-loading="loading" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4">
        <IdCard
            v-for="account in accounts"
            :key="account.id"
            :availability="account.status"
            :account="account.email"
            :password="account.password"
            :country="account.country"
        />
      </div>
    </el-scrollbar>

  </div>
  <Collapse></Collapse>

</template>

<script>
import IdCard from "@/components/IdCard.vue";
import axios from "axios";
import {ChatLineRound} from "@element-plus/icons-vue";
import Statistic from "@/components/Statistic.vue";

import Collapse from "@/components/Collapse.vue";


export default {
  name: 'AccountsContainer',
  components: {
    Collapse,
    Statistic,
    ChatLineRound,
    IdCard
  },
  data() {
    return {
      accounts: [],
      items: [
        "所有id均来自于网络搜集",
        "禁止在设置中进行登录",
        "只能在桌面AppStore内登录ID",
        "请认真查看页面中的使用步骤",
      ],
      centerDialogVisible: true,
      loading: true,
      pagePv: 0,
      pageUv: 0
    }
  },
  methods:{
    goToGitHub(){
      window.open('https://github.com/Bear-biscuit/ID_SharedWeb', '_blank');
    }
  },
  async created() {

    try {
      // 小火箭账号
      const reData = await axios({url: import.meta.env.VITE_API_URL})
      this.accounts = reData.data.id
      this.loading = false
    } catch (error) {
      this.loading = false
    }
    try {
      // 访问统计
      const reData = await axios({
        url: 'https://webviso.yestool.org/api/visit',
        method: 'POST',
        data: {
          "url": "/",
          "hostname": import.meta.env.VITE_APP_DOMAIN,
          "referrer": "",
          "pv": true,
          "uv": true
        }
      });

      this.pagePv = reData.data.data.pv
      this.pageUv = reData.data.data.uv
    } catch (error) {
      console.log(error);
    }

  }
}
</script>
