<template>
  <main class="w-full max-w-6xl mx-auto px-4 pt-12 pb-20">
    
    <div class="relative z-20 bg-white rounded-3xl shadow-sm hover:shadow-md transition-shadow p-8 mb-8 flex flex-col md:flex-row items-center justify-between mt-[-40px]">
      <div>
        <h2 class="text-3xl font-bold text-gray-800 mb-4 font-chinese">这是我们一起走过的</h2>
        <div class="flex items-center gap-2 text-sm text-gray-500 bg-red-50 px-4 py-1.5 rounded-full w-max">
          <i class="fa-solid fa-heart text-red-400"></i>
          <span class="font-bold">TOGETHER SINCE</span> 2023-07-19
        </div>
      </div>
      
      <div class="text-center mt-6 md:mt-0 font-sans">
        <div class="text-7xl font-black text-gray-800 tracking-tighter">
          {{ timer.days }}<span class="text-sm font-normal text-gray-400 ml-2 tracking-normal">DAYS</span>
        </div>
        <div class="flex gap-6 mt-3 justify-center text-gray-600 font-bold">
          <div class="flex flex-col items-center"><span class="text-2xl">{{ timer.hours }}</span><span class="text-[10px] text-gray-400 font-normal">HOURS</span></div>
          <div class="flex flex-col items-center"><span class="text-2xl">{{ timer.minutes }}</span><span class="text-[10px] text-gray-400 font-normal">MINUTES</span></div>
          <div class="flex flex-col items-center"><span class="text-2xl">{{ timer.seconds }}</span><span class="text-[10px] text-gray-400 font-normal">SECONDS</span></div>
        </div>
      </div>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-4 gap-4 font-chinese">
      
      <div class="md:col-span-2 md:row-span-2 bg-[#18181A] text-white rounded-3xl p-6 relative flex flex-col justify-end min-h-[320px] overflow-hidden group cursor-pointer">
        <div class="absolute top-5 left-5 flex items-center gap-3 z-10">
           <img src="https://api.dicebear.com/7.x/notionists/svg?seed=Ki" alt="avatar" class="w-8 h-8 rounded-full bg-white/10 p-1">
           <span class="text-sm text-gray-300">回忆中...</span>
        </div>
        <div class="z-10 transition-transform duration-300 group-hover:translate-y-[-5px]">
          <h3 class="text-2xl font-bold mb-2">时光碎片</h3>
          <p class="text-gray-400 text-sm">网络小差，请稍后重试</p>
        </div>
        <div class="absolute inset-0 bg-gradient-to-t from-black/80 to-transparent"></div>
      </div>

      <div class="bg-blue-500 text-white rounded-3xl p-6 flex flex-col justify-between hover:bg-blue-600 transition-colors cursor-pointer">
        <div class="flex justify-between items-center"><span class="font-bold">Ki.</span><i class="fa-solid fa-cloud-sun text-xl"></i></div>
        <div class="text-4xl font-bold mt-6">--°</div>
        <div class="text-xs text-blue-100 mt-2 flex items-center gap-1"><i class="fa-solid fa-location-dot"></i> 离线</div>
      </div>

      <div class="bg-orange-400 text-white rounded-3xl p-6 flex flex-col justify-between hover:bg-orange-500 transition-colors cursor-pointer">
         <div class="flex justify-between items-center"><span class="font-bold">Really</span><i class="fa-solid fa-sun text-xl"></i></div>
         <div class="text-4xl font-bold mt-6">--°</div>
         <div class="text-xs text-orange-100 mt-2 flex items-center gap-1"><i class="fa-solid fa-location-dot"></i> 离线</div>
      </div>

      <div class="md:col-span-2 bg-[#7D8592] text-white rounded-3xl p-6 flex flex-col justify-between relative overflow-hidden">
         <i class="fa-solid fa-star absolute right-[-20px] bottom-[-20px] text-8xl text-white/10 transform rotate-12"></i>
         <div class="flex justify-between text-sm opacity-90">
           <span class="flex items-center gap-2"><i class="fa-solid fa-list-check"></i> 恋爱清单</span>
           <span>我们的约定</span>
         </div>
         <div class="mt-8 flex items-end justify-between relative z-10">
           <div class="text-4xl font-bold">17<span class="text-xl text-gray-300 font-normal"> / 29</span></div>
           <div class="text-3xl font-bold">59<span class="text-lg font-normal">%</span></div>
         </div>
         <div class="w-full bg-white/20 h-2.5 rounded-full mt-4 relative z-10 overflow-hidden">
           <div class="bg-white h-full rounded-full w-[59%] transition-all duration-1000 ease-out"></div>
         </div>
      </div>

      <div 
        v-for="card in statsCards" 
        :key="card.id" 
        :class="[card.bgColor, 'text-white rounded-3xl p-6 flex flex-col justify-between hover:-translate-y-1 hover:shadow-lg transition-all duration-300 cursor-pointer']"
      >
        <div class="text-xs opacity-80 flex items-center gap-2 font-medium">
          <i :class="card.icon"></i> {{ card.title }}
        </div>
        <div class="mt-6">
          <div class="text-4xl font-bold">{{ card.value }}</div>
          <div class="text-xs opacity-70 mt-1">{{ card.subtitle }}</div>
        </div>
      </div>

    </div>
  </main>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue';

// ==========================================
// 1. 计时器逻辑 (精确到秒)
// ==========================================
const startDate = new Date('2023-07-19T00:00:00').getTime();
const timer = reactive({ days: '00', hours: '00', minutes: '00', seconds: '00' });
let countdownInterval = null;

// 补零工具函数 (把 9 变成 09)
const padZero = (num) => (num < 10 ? `0${num}` : num);

const updateTimer = () => {
  const now = new Date().getTime();
  const distance = now - startDate;
  
  if (distance > 0) {
    timer.days = Math.floor(distance / (1000 * 60 * 60 * 24));
    timer.hours = padZero(Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)));
    timer.minutes = padZero(Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60)));
    timer.seconds = padZero(Math.floor((distance % (1000 * 60)) / 1000));
  }
};

// ==========================================
// 2. 数据驱动的统计卡片 (非常方便从后端获取数据后直接覆盖)
// ==========================================
const statsCards = ref([
  { id: 1, title: '日常点滴', subtitle: '文章数量', value: '5', bgColor: 'bg-[#6B6358]', icon: 'fa-solid fa-book-open' },
  { id: 2, title: '回忆相册', subtitle: '照片数量', value: '117', bgColor: 'bg-[#3B82F6]', icon: 'fa-solid fa-images' },
  { id: 3, title: '祝福留言', subtitle: '收到的祝福', value: '150', bgColor: 'bg-[#F43F5E]', icon: 'fa-solid fa-envelope-open-text' },
  { id: 4, title: '恋爱大事记', subtitle: '时光轴事件', value: '0', bgColor: 'bg-[#111827]', icon: 'fa-solid fa-flag-checkered' }
]);

// ==========================================
// 生命周期钩子
// ==========================================
onMounted(() => {
  updateTimer(); // 初始化立即执行一次
  countdownInterval = setInterval(updateTimer, 1000); // 每秒更新
});

onUnmounted(() => {
  if (countdownInterval) clearInterval(countdownInterval);
});
</script>