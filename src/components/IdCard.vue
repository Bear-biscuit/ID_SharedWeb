<template>
  <div class="bg-white shadow-sm rounded-md p-3 h-40 flex flex-col justify-between">
    <div>
      <div class="flex justify-between items-center mb-2">
        <h2 class="text-sm font-semibold text-gray-800">{{ country }}-{{flagEmoji}}</h2>
        <span class="text-xs px-2 py-0.5  text-green-800 rounded"
              :class="{
          'bg-green-100':availability==='正常',
          'bg-red-100':availability!=='正常',
        }">{{ availability }}</span>
      </div>
      <div class="mb-2">
        <p class="text-xs text-gray-600 truncate">账号: {{ account }}</p>
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

<script setup>
import {ElMessage, ElNotification} from "element-plus";
import {computed, ref} from "vue";

const isShow = ref(false)

// 国家和旗帜代码映射
const countryCode = {
  "中国": "CN",
  "中国大陆": "CN",
  "台湾": "CN",
  "香港": "CN",
  "澳门": "CN",
  "美国": "US",
  "日本": "JP",
  "德国": "DE",
  "印度": "IN",
  "法国": "FR",
  "英国": "GB",
  "加拿大": "CA",
  "澳大利亚": "AU",
  "俄罗斯": "RU",
  "巴西": "BR",
  "意大利": "IT",
  "西班牙": "ES",
  "墨西哥": "MX",
  "韩国": "KR",
  "阿根廷": "AR",
  "南非": "ZA",
  "荷兰": "NL",
  "瑞士": "CH",
  "瑞典": "SE",
  "挪威": "NO",
  "比利时": "BE",
  "葡萄牙": "PT",
  "新加坡": "SG",
  "新西兰": "NZ",
  "土耳其": "TR",
  "沙特阿拉伯": "SA",
  "阿联酋": "AE",
  "印度尼西亚": "ID",
  "马来西亚": "MY",
  "泰国": "TH",
  "菲律宾": "PH",
  "越南": "VN",
  "埃及": "EG",
  "肯尼亚": "KE",
  "乌克兰": "UA",
  "波兰": "PL",
  "捷克": "CZ",
  "匈牙利": "HU",
  "奥地利": "AT",
  "希腊": "GR",
  "丹麦": "DK",
  "芬兰": "FI",
  "爱尔兰": "IE",
  "以色列": "IL",
  "黎巴嫩": "LB",
  "卡塔尔": "QA",
  "巴基斯坦": "PK",
  "孟加拉国": "BD",
  "斯里兰卡": "LK",
  "巴勒斯坦": "PS",
  "阿尔及利亚": "DZ",
  "摩洛哥": "MA",
  "突尼斯": "TN",
  "利比亚": "LY",
  "安哥拉": "AO",
  "尼日利亚": "NG",
  "坦桑尼亚": "TZ",
  "乌干达": "UG",
  "加纳": "GH",
  "喀麦隆": "CM",
  "科特迪瓦": "CI",
  "塞内加尔": "SN",
  "津巴布韦": "ZW"
};

const props = defineProps({
  availability: String,
  account: String,
  password: String,
  country: true
})

// 计算属性，根据国家名称获取对应的旗帜 emoji
const flagEmoji = computed(() => {
  const code = countryCode[props.country];
  if (!code) {
    return '💫';
  }
  // 将国家代码转换为两个 Unicode 字符来显示旗帜 emoji
  return code.split('')
      .map(letter => String.fromCodePoint(0x1F1E6 - 65 + letter.charCodeAt(0)))
      .join('');
})

const copyText = (text) => {
  try {
    navigator.clipboard.writeText(text);
    openS()
  } catch (err) {
    console.error('复制出错', err);
    openE()
  }
}

const openS = () => {
  ElNotification({
    title: 'Success',
    message: '复制成功',
    type: 'success',
    duration: 2000,
  })
}

const openE = () => {
  ElNotification({
    title: 'Error',
    message: '复制失败',
    type: 'error',
    duration: 2000,
  })
}
</script>
