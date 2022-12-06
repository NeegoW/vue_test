<template>
  <div class="home">
    <h1 @click="addUrl(5)">This is an Home page</h1>
  </div>
  <section style="width:60%;margin: 20px auto">
    <el-row :gutter="10">
      <el-col :span="12">
        <el-row class="wtf-1">
          <el-col class="viewpoint">
            <img v-for="u in banner" class="img" :key="u" :src="u" :alt="u">
          </el-col>
          <el-col v-for="(u,k) in ch1" :key="k">
            <img :src="u" :alt="u">
          </el-col>
        </el-row>
      </el-col>
      <el-col :span="12">
        <el-row class="wtf-2">
          <el-col v-for="(u,k) in ch2" :key="k">
            <img :src="u" :alt="u">
          </el-col>
        </el-row>
      </el-col>
    </el-row>
  </section>
</template>

<script setup>
import { reactive, onMounted, computed } from 'vue'

// banner地址
const banner = [
  'https://images5.alphacoders.com/587/thumbbig-587597.webp',
  'https://images6.alphacoders.com/596/thumbbig-596848.webp',
  'https://images3.alphacoders.com/111/thumbbig-1116286.webp',
  'https://images5.alphacoders.com/113/thumbbig-1134110.webp'
]
// 用于存放图片地址，用于在页面上显示
const urls = reactive([])
const demo = [
  'https://images3.alphacoders.com/102/102135.jpg',
  'https://images2.alphacoders.com/102/102970.jpg',
  'https://images2.alphacoders.com/661/661667.png',
  'https://images4.alphacoders.com/606/606667.jpg',
  'https://images6.alphacoders.com/606/606263.jpg',
  'https://images5.alphacoders.com/606/606284.jpg',
  'https://images.alphacoders.com/183/183401.jpg',
  'https://images7.alphacoders.com/311/311022.jpg',
  'https://images4.alphacoders.com/966/96656.jpg',
  'https://images8.alphacoders.com/505/505303.jpg'
]
const ch1 = computed(() => {
  // 因为左边列有一个图片，所以左边栏为urls的奇数内容，右边栏为偶数内容
  return urls.filter((u, k) => k % 2 === 1)
})
const ch2 = computed(() => {
  return urls.filter((u, k) => k % 2 === 0)
})

const addUrl = (n) => {
  for (let i = 0; i < n; i++) {
    const j = Math.floor(Math.random() * demo.length)
    urls.push(demo[j])
  }
}

onMounted(() => {
  // 从demo中随机取出4张图片，用于在页面上显示
  addUrl(4)
})
</script>

<style lang="scss">
@keyframes tonext {
  75% {
    left: 0;
  }
  95% {
    left: 100%;
  }
  98% {
    left: 100%;
  }
  99% {
    left: 0;
  }
}

@keyframes snap {
  96% {
    scroll-snap-align: center;
  }
  97% {
    scroll-snap-align: none;
  }
  99% {
    scroll-snap-align: none;
  }
  100% {
    scroll-snap-align: center;
  }
}

.viewpoint {
  display: flex;
  overflow: auto;
  scroll-behavior: smooth;
  scroll-snap-type: x mandatory;

  .img {
    width: 100%;
    flex-shrink: 0;
    scroll-snap-align: start;
  }
}

.wtf-1 {
  background-color: #4290e2;
}

.wtf-2 {
  background-color: #42b983;
}

img {
  width: 100%;
}
</style>
