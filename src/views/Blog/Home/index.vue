<template>
  <div class="lg-newui-app font-chinese text-gray-800 bg-[#F8F9FA] min-h-screen relative">
    
    <Transition name="sticky-bar">
      <header v-show="isScrolled" class="fixed top-0 left-0 w-full z-50 h-[72px] px-6 flex items-center justify-between bg-white/80 backdrop-blur-xl border-b border-white/20 shadow-sm">
        <div class="nav-left flex items-center gap-3">
          <div class="bg-black/90 text-white px-4 py-1.5 rounded-full flex items-center gap-2 shadow-md">
            <span class="font-bold text-sm tracking-widest">Ki.</span>
            <div class="flex items-center text-red-500"><i class="fa-solid fa-heart text-xs animate-pulse"></i></div>
            <span class="font-bold text-sm tracking-widest">Really</span>
          </div>
        </div>
        
        <nav class="nav-center hidden md:flex items-center bg-white/90 backdrop-blur-md rounded-full p-1.5 shadow-sm border border-gray-100">
          <a v-for="item in navItems" :key="item.name" href="#" :class="['px-5 py-2 rounded-full text-[13px] font-medium transition-all duration-300 flex items-center gap-2', item.isHome ? 'bg-red-400 text-white shadow-md shadow-red-200 transform hover:scale-105' : 'text-gray-600 hover:bg-gray-100/80']">
             <i :class="item.icon" :style="item.isHome ? '' : 'font-size: 12px;'"></i>
             <span>{{ item.name }}</span>
          </a>
        </nav>

        <div class="nav-right flex items-center gap-4">
           <div class="w-9 h-9 rounded-full overflow-hidden border-2 border-white shadow-sm cursor-pointer hover:scale-110 transition-transform">
             <img src="https://api.dicebear.com/7.x/notionists/svg?seed=Ki&backgroundColor=e2e8f0" class="w-full h-full object-cover">
           </div>
        </div>
      </header>
    </Transition>

    <section class="relative w-full h-[100vh] max-h-[800px] min-h-[400px] overflow-hidden bg-gray-900 flex flex-col items-center justify-center">
      <div class="absolute inset-0 w-full h-full z-0">
        <div v-for="(img, index) in bannerImages" :key="index" :class="['absolute inset-0 w-full h-full bg-cover bg-center transition-opacity duration-1500 ease-in-out', currentIndex === index ? 'opacity-100' : 'opacity-0']" :style="{ backgroundImage: `url(${img})` }">
          <div class="absolute inset-0 bg-black/30"></div>
        </div>
      </div>

      <div class="absolute top-0 w-full text-center py-8 z-20">
        <h1 class="font-cursive text-3xl font-bold text-white tracking-widest drop-shadow-md lg-title-highlight">春和景明</h1>
      </div>

      <div class="relative z-20 flex items-center justify-center gap-4 md:gap-10 mt-[-5vh]">
         <div class="relative flex flex-col items-center group w-[120px] h-[120px] md:w-[150px] md:h-[150px]">
            <img src="https://loveli.kikiw.cn/Style/img/wreath.png" class="absolute inset-0 w-full h-full animate-[spin_12s_linear_infinite] opacity-90 scale-125 pointer-events-none" alt="wreath">
            <div class="w-[85px] h-[85px] md:w-[110px] md:h-[110px] rounded-full border-[3px] border-white/70 p-1 shadow-2xl overflow-hidden mt-4 md:mt-5 transition-transform duration-300 group-hover:scale-105">
               <img src="https://api.dicebear.com/7.x/notionists/svg?seed=Ki" class="w-full h-full object-cover rounded-full bg-white">
            </div>
            <div class="absolute -bottom-2 bg-black/60 backdrop-blur-md text-white px-5 py-1 rounded-full text-xs font-bold shadow-lg tracking-widest">Ki.</div>
         </div>
         
         <div class="text-rose-500 text-5xl md:text-6xl drop-shadow-[0_0_15px_rgba(244,63,94,0.6)] animate-pulse mx-2"><i class="fa-solid fa-heart"></i></div>
         
         <div class="relative flex flex-col items-center group w-[120px] h-[120px] md:w-[150px] md:h-[150px]">
            <img src="https://loveli.kikiw.cn/Style/img/wreath.png" class="absolute inset-0 w-full h-full animate-[spin_12s_linear_infinite_reverse] opacity-90 scale-125 pointer-events-none" alt="wreath">
            <div class="w-[85px] h-[85px] md:w-[110px] md:h-[110px] rounded-full border-[3px] border-white/70 p-1 shadow-2xl overflow-hidden mt-4 md:mt-5 transition-transform duration-300 group-hover:scale-105">
               <img src="https://api.dicebear.com/7.x/notionists/svg?seed=Really" class="w-full h-full object-cover rounded-full bg-white">
            </div>
            <div class="absolute -bottom-2 bg-black/60 backdrop-blur-md text-white px-5 py-1 rounded-full text-xs font-bold shadow-lg tracking-widest">Really</div>
         </div>
      </div>

      <div ref="originalMenuRef" :class="['relative z-20 mt-16 md:mt-24 transition-all duration-700', isScrolled ? 'opacity-0 translate-y-12 pointer-events-none scale-95' : 'opacity-100 translate-y-0 scale-100']">
         <nav class="flex flex-wrap items-center justify-center gap-5 md:gap-10 px-4">
            <a v-for="item in navItems" :key="item.name" href="#" class="group flex flex-col items-center gap-2">
               <div :class="['flex items-center justify-center rounded-full shadow-lg transition-all duration-300 group-hover:-translate-y-2', item.isHome ? 'w-14 h-14 md:w-16 md:h-16 bg-rose-500 text-white text-2xl shadow-rose-500/40' : 'w-11 h-11 md:w-12 md:h-12 bg-white/90 backdrop-blur-md text-gray-700 text-lg hover:bg-white']"><i :class="item.icon"></i></div>
               <span v-if="!item.isHome" class="text-white/90 text-xs font-medium tracking-wide drop-shadow-md">{{ item.name }}</span>
            </a>
         </nav>
      </div>

      <div class="absolute bottom-[10%] w-full flex justify-center space-x-2 z-20">
        <button v-for="(_, index) in bannerImages" :key="index" @click="setSlide(index)" :class="['h-1.5 rounded-full transition-all duration-500', currentIndex === index ? 'w-6 bg-white' : 'w-1.5 bg-white/40']"></button>
      </div>

      <div class="absolute bottom-0 left-0 w-full z-10 leading-none">
        <svg class="waves block w-full h-[60px] md:h-[100px]" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 24 150 28" preserveAspectRatio="none" shape-rendering="auto"><defs><path id="gentle-wave" d="M-160 44c30 0 58-18 88-18s 58 18 88 18 58-18 88-18 58 18 88 18 v44h-352z" /></defs><g class="parallax"><use xlink:href="#gentle-wave" x="48" y="0" fill="rgba(248, 249, 250, 0.7)" /><use xlink:href="#gentle-wave" x="48" y="3" fill="rgba(248, 249, 250, 0.5)" /><use xlink:href="#gentle-wave" x="48" y="5" fill="rgba(248, 249, 250, 0.3)" /><use xlink:href="#gentle-wave" x="48" y="7" fill="#F8F9FA" /></g></svg>
      </div>
    </section>

    <main class="w-full max-w-[1100px] mx-auto px-4 pb-20 relative z-30 mt-[-40px] space-y-20">
       
       <section v-slide-up>
         <div class="bg-white rounded-[2rem] p-8 md:p-12 shadow-[0_10px_40px_-10px_rgba(0,0,0,0.05)] flex flex-col md:flex-row justify-between items-center mb-8 relative overflow-hidden group">
            <div class="absolute -top-32 -right-32 w-96 h-96 bg-rose-50 rounded-full blur-3xl opacity-70 pointer-events-none"></div>
            <div class="relative z-10 flex flex-col items-center md:items-start gap-8 w-full md:w-auto text-center md:text-left">
               <h2 class="text-3xl md:text-[34px] font-bold text-[#2C2E33] tracking-widest lg-font-serif">这是我们一起走过的</h2>
               <div class="flex items-center gap-4">
                 <div class="w-10 h-10 rounded-full bg-[#FA5252] flex items-center justify-center shadow-lg shadow-red-200"><i class="fa-solid fa-heart text-white text-[15px]"></i></div>
                 <div class="flex flex-col justify-center text-left">
                   <span class="text-[9px] text-gray-400 font-bold tracking-[0.2em]">TOGETHER SINCE</span>
                   <span class="text-[13px] font-bold text-gray-600">2023-07-19 00:00</span>
                 </div>
               </div>
            </div>
            <div class="relative z-10 flex flex-col items-center mt-12 md:mt-0 font-sans">
               <div class="flex flex-col items-center justify-center mb-6">
                 <span class="text-7xl md:text-[85px] leading-[0.85] font-black text-[#2A303C] tracking-tighter">{{ timer.days }}</span>
                 <div class="w-8 h-[3px] bg-[#FA5252] mt-5 mb-3 rounded-full opacity-90"></div>
                 <span class="text-[10px] text-[#FA5252] tracking-[0.3em] font-bold">DAYS</span>
               </div>
               <div class="flex gap-8 text-[#2A303C]">
                 <div class="flex flex-col items-center w-12"><span class="text-[26px] font-bold leading-none">{{ timer.hours }}</span><span class="text-[9px] text-gray-400 tracking-[0.15em] mt-2 font-medium">HOURS</span></div>
                 <div class="flex flex-col items-center w-12"><span class="text-[26px] font-bold leading-none">{{ timer.minutes }}</span><span class="text-[9px] text-gray-400 tracking-[0.15em] mt-2 font-medium">MINUTES</span></div>
                 <div class="flex flex-col items-center w-12"><span class="text-[26px] font-bold leading-none">{{ timer.seconds }}</span><span class="text-[9px] text-gray-400 tracking-[0.15em] mt-2 font-medium">SECONDS</span></div>
               </div>
            </div>
         </div>

         <div class="grid grid-cols-1 md:grid-cols-4 gap-4 md:gap-5">
            <div class="md:col-span-2 md:row-span-2 bg-[#18181A] text-white rounded-[24px] p-6 relative flex flex-col justify-end min-h-[340px] overflow-hidden group cursor-pointer shadow-sm">
               <div class="absolute inset-0 bg-[url('https://images.unsplash.com/photo-1518837695005-2083093ee35b?q=80&w=800')] bg-cover bg-center opacity-40 transition-transform duration-700 group-hover:scale-105"></div>
               <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/20 to-transparent"></div>
               <div class="absolute top-5 left-5 flex items-center gap-3 z-10 bg-white/10 backdrop-blur-sm px-3 py-1.5 rounded-full">
                  <div class="w-1.5 h-1.5 rounded-full bg-green-400 animate-pulse"></div>
                  <span class="text-[11px] text-gray-200 font-medium">回忆中...</span>
               </div>
               <div class="z-10 transition-transform duration-300 group-hover:-translate-y-1">
                 <h3 class="text-2xl font-bold mb-2 tracking-widest">时光碎片</h3>
                 <p class="text-gray-300 text-xs flex items-center gap-2"><i class="fa-regular fa-image"></i> 117 张照片记录</p>
               </div>
            </div>
            <div v-for="card in statsCards" :key="card.id" :class="[card.bg, 'text-white rounded-[24px] p-6 flex flex-col justify-between shadow-sm hover:shadow-lg transition-all hover:-translate-y-1 cursor-pointer']">
              <div class="text-[11px] opacity-80 flex items-center gap-1.5 font-medium tracking-wide">
                 <i :class="card.icon"></i> {{ card.title }}
              </div>
              <div class="mt-6">
                 <div class="text-3xl font-bold tracking-tight">{{ card.value }}</div>
                 <div class="text-[10px] opacity-70 mt-1 uppercase">{{ card.subtitle }}</div>
              </div>
            </div>
         </div>
       </section>

       <section>
          <div class="text-center mb-10" v-slide-up>
             <h2 class="text-3xl font-bold text-gray-800 lg-font-serif tracking-widest">Love Day</h2>
             <p class="text-sm text-gray-400 mt-2 font-cursive">100 Things To Do With You</p>
             <div class="flex justify-center mt-3"><div class="w-12 h-1 bg-rose-400 rounded-full"></div></div>
          </div>
          
          <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-5 gap-4">
             <div v-for="(item, index) in loveDayList" :key="item.id" v-slide-up :style="{ transitionDelay: `${(index % 5) * 100}ms` }"
                  :class="['relative rounded-[20px] p-4 flex flex-col justify-between items-center text-center overflow-hidden shadow-sm hover:shadow-md transition-all hover:-translate-y-1 cursor-pointer group', item.done ? 'bg-rose-50 border border-rose-100' : 'bg-white border border-dashed border-gray-200']">
                <div class="absolute top-2 left-2 text-[10px] font-bold text-gray-300">{{ index + 1 }}</div>
                <div :class="['w-10 h-10 rounded-full flex items-center justify-center mb-2 mt-3 transition-transform group-hover:scale-110', item.done ? 'bg-rose-400 text-white shadow-md shadow-rose-200' : 'bg-gray-100 text-gray-300']">
                   <i :class="item.icon"></i>
                </div>
                <h3 class="text-xs font-bold tracking-wide" :class="item.done ? 'text-gray-800' : 'text-gray-400'">{{ item.title }}</h3>
                <i v-if="item.done" class="fa-solid fa-check text-green-400 absolute top-2 right-2 text-xs"></i>
             </div>
          </div>
       </section>

       <section>
          <div class="text-center mb-10" v-slide-up>
             <h2 class="text-3xl font-bold text-gray-800 lg-font-serif tracking-widest">日常点滴</h2>
             <p class="text-sm text-gray-400 mt-2 font-cursive">Our Daily Memories</p>
             <div class="flex justify-center mt-3"><div class="w-12 h-1 bg-blue-400 rounded-full"></div></div>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
             <article v-for="(article, index) in articles" :key="index" v-slide-up :style="{ transitionDelay: `${index * 150}ms` }"
                      class="bg-white rounded-[24px] overflow-hidden shadow-[0_8px_30px_rgb(0,0,0,0.04)] hover:shadow-[0_15px_40px_rgb(0,0,0,0.08)] transition-all duration-500 hover:-translate-y-2 cursor-pointer group">
                <div class="relative h-48 overflow-hidden">
                   <div class="absolute inset-0 bg-cover bg-center transition-transform duration-700 group-hover:scale-105" :style="{ backgroundImage: `url(${article.cover})` }"></div>
                   <div class="absolute top-4 left-4 bg-white/90 backdrop-blur-sm px-3 py-1 rounded-full text-[11px] font-bold text-gray-700 shadow-sm flex items-center gap-1.5"><i class="fa-regular fa-calendar-days text-blue-400"></i> {{ article.date }}</div>
                </div>
                <div class="p-6">
                   <h3 class="text-lg font-bold text-gray-800 mb-2 group-hover:text-blue-500 transition-colors">{{ article.title }}</h3>
                   <p class="text-xs text-gray-500 leading-relaxed line-clamp-2">{{ article.desc }}</p>
                </div>
             </article>
          </div>
       </section>

       <section>
          <div class="text-center mb-10" v-slide-up>
             <h2 class="text-3xl font-bold text-gray-800 lg-font-serif tracking-widest">回忆相册</h2>
             <p class="text-sm text-gray-400 mt-2 font-cursive">Gallery of Love</p>
             <div class="flex justify-center mt-3"><div class="w-12 h-1 bg-orange-400 rounded-full"></div></div>
          </div>

          <div class="columns-2 md:columns-3 lg:columns-4 gap-4 space-y-4">
             <div v-for="(photo, index) in photos" :key="index" v-slide-up :style="{ transitionDelay: `${(index % 4) * 100}ms` }"
                  class="relative break-inside-avoid rounded-[16px] overflow-hidden group cursor-zoom-in shadow-sm hover:shadow-lg transition-all">
                <img :src="photo" class="w-full h-auto object-cover transition-transform duration-700 group-hover:scale-110" loading="lazy">
                <div class="absolute inset-0 bg-black/0 group-hover:bg-black/20 transition-colors duration-300 flex items-center justify-center">
                   <i class="fa-solid fa-magnifying-glass-plus text-white text-3xl opacity-0 group-hover:opacity-100 transition-all duration-300 transform scale-50 group-hover:scale-100"></i>
                </div>
             </div>
          </div>
       </section>

       <section>
          <div class="text-center mb-10" v-slide-up>
             <h2 class="text-3xl font-bold text-gray-800 lg-font-serif tracking-widest">祝福留言</h2>
             <p class="text-sm text-gray-400 mt-2 font-cursive">Leave a Message</p>
             <div class="flex justify-center mt-3"><div class="w-12 h-1 bg-green-400 rounded-full"></div></div>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
             <div class="bg-white rounded-[24px] p-6 md:p-8 shadow-sm border border-gray-100" v-slide-up>
                <textarea rows="4" class="w-full bg-[#F8F9FA] rounded-xl p-4 text-sm text-gray-700 border-none focus:ring-2 focus:ring-green-200 resize-none transition-shadow" placeholder="写下你们的祝福..."></textarea>
                <div class="flex justify-between items-center mt-4">
                   <div class="flex gap-2 text-gray-400">
                     <button class="hover:text-gray-600 transition-colors"><i class="fa-regular fa-face-smile text-xl"></i></button>
                     <button class="hover:text-gray-600 transition-colors"><i class="fa-regular fa-image text-xl"></i></button>
                   </div>
                   <button class="bg-green-400 hover:bg-green-500 text-white px-6 py-2 rounded-full text-sm font-bold shadow-md shadow-green-200 transition-all hover:-translate-y-1">发送祝福</button>
                </div>
             </div>

             <div class="space-y-4 h-[280px] overflow-y-auto pr-2 custom-scrollbar">
                <div v-for="(comment, index) in comments" :key="index" v-slide-up :style="{ transitionDelay: `${index * 100}ms` }"
                     class="bg-white rounded-2xl p-4 flex gap-4 shadow-[0_2px_10px_rgb(0,0,0,0.02)]">
                   <img :src="comment.avatar" class="w-10 h-10 rounded-full bg-gray-100 border border-gray-100">
                   <div>
                      <div class="flex items-center gap-2 mb-1">
                        <span class="text-sm font-bold text-gray-700">{{ comment.name }}</span>
                        <span class="text-[10px] text-gray-400">{{ comment.time }}</span>
                      </div>
                      <p class="text-sm text-gray-600 leading-relaxed">{{ comment.text }}</p>
                   </div>
                </div>
             </div>
          </div>
       </section>

    </main>

    <footer class="bg-white border-t border-gray-100 mt-20 py-12" v-slide-up>
       <div class="max-w-[1100px] mx-auto px-4 flex flex-col items-center justify-center text-center">
          <div class="flex items-center gap-2 text-2xl font-bold mb-4 font-cursive text-gray-800">
             <span>Ki</span>
             <i class="fa-solid fa-heart text-rose-500 animate-pulse text-sm mx-1"></i>
             <span>Really</span>
          </div>
          <p class="text-xs text-gray-500 mb-3 tracking-widest">收好我们的日常与心动</p>
          <div class="flex flex-wrap items-center justify-center gap-4 text-[11px] text-gray-400 mt-2 font-medium">
             <span>© 2024 Our Cozy Place.</span>
             <a href="#" class="hover:text-gray-700 transition-colors">萌ICP备20230000号</a>
             <span class="bg-gray-100 px-2 py-1 rounded">已平稳运行 {{ timer.days }} 天</span>
          </div>
       </div>
    </footer>

    <Transition name="fade-slide">
      <button 
        v-show="showBackToTop" 
        @click="scrollToTop"
        class="fixed bottom-10 right-8 md:right-10 w-12 h-12 bg-blue-500 text-white rounded-full flex items-center justify-center shadow-[0_5px_20px_rgba(59,130,246,0.4)] hover:bg-blue-600 transition-all duration-300 z-50 group hover:-translate-y-2 cursor-pointer border-2 border-white"
        title="回到顶部"
      >
        <i class="fa-solid fa-arrow-up text-lg group-hover:animate-bounce"></i>
      </button>
    </Transition>

  </div>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue';

// 自定义指令：上涌动画 v-slide-up
const vSlideUp = {
  mounted(el) {
    el.classList.add('opacity-0', 'translate-y-16', 'transition-all', 'duration-[800ms]', 'ease-[cubic-bezier(0.25,0.8,0.25,1)]');
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          el.classList.remove('opacity-0', 'translate-y-16');
          el.classList.add('opacity-100', 'translate-y-0');
          observer.unobserve(el);
        }
      });
    }, { threshold: 0.1 });
    observer.observe(el);
  }
};

// ==========================================
// 状态与数据管理
// ==========================================
const isScrolled = ref(false);
const showBackToTop = ref(false);
const originalMenuRef = ref(null);

const navItems = [
  { name: '点滴', icon: 'fa-solid fa-droplet' },
  { name: '留言', icon: 'fa-solid fa-message' },
  { name: '轨迹', icon: 'fa-solid fa-shoe-prints' },
  { name: '首页', icon: 'fa-solid fa-house', isHome: true },
  { name: '相册', icon: 'fa-solid fa-camera-retro' },
  { name: '清单', icon: 'fa-solid fa-list-check' },
  { name: '关于', icon: 'fa-solid fa-circle-info' }
];

const bannerImages = ref([
  'https://images.unsplash.com/photo-1518837695005-2083093ee35b?q=80&w=2000&auto=format&fit=crop', 
  'https://images.unsplash.com/photo-1473448912268-2022ce9509d8?q=80&w=2000&auto=format&fit=crop'
]);
const currentIndex = ref(0);
let autoPlayTimer = null;
const setSlide = (index) => { currentIndex.value = index; };
const nextSlide = () => { currentIndex.value = (currentIndex.value + 1) % bannerImages.value.length; };

// 回到顶部方法
const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
};

// 滚动监听逻辑
const handleScroll = () => {
  const scrollY = window.scrollY;
  // 1. 控制顶部 Header 出现
  if (originalMenuRef.value) {
    const rect = originalMenuRef.value.getBoundingClientRect();
    isScrolled.value = rect.top <= 72;
  }
  // 2. 控制右下角“回顶”按钮出现 (滚动超过 600px 时显示)
  showBackToTop.value = scrollY > 600;
};

// 计时器
const startDate = new Date('2023-07-19T00:00:00').getTime();
const timer = reactive({ days: '0', hours: '00', minutes: '00', seconds: '00' });
let countdownInterval = null;
const padZero = (num) => (num < 10 ? `0${num}` : num);
const updateTimer = () => {
  const distance = new Date().getTime() - startDate;
  if (distance > 0) {
    timer.days = Math.floor(distance / (1000 * 60 * 60 * 24));
    timer.hours = padZero(Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)));
    timer.minutes = padZero(Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60)));
    timer.seconds = padZero(Math.floor((distance % (1000 * 60)) / 1000));
  }
};

// 统计 Bento 数据
const statsCards = ref([
  { id: 1, title: '恋爱天气', subtitle: '深圳', value: '28°', bg: 'bg-gradient-to-br from-blue-400 to-blue-500', icon: 'fa-solid fa-cloud-sun' },
  { id: 2, title: '恋爱天气', subtitle: '东莞', value: '26°', bg: 'bg-gradient-to-br from-orange-400 to-orange-500', icon: 'fa-solid fa-sun' },
  { id: 3, title: '完成约定', subtitle: 'Love List', value: '17/29', bg: 'bg-[#7D8592] md:col-span-2', icon: 'fa-solid fa-list-check' },
]);

// Love Day (100件小事) 数据
const loveDayList = ref([
  { id: 1, title: '一起看日出', icon: 'fa-solid fa-sun', done: true },
  { id: 2, title: '养一只猫猫', icon: 'fa-solid fa-cat', done: true },
  { id: 3, title: '穿情侣装逛街', icon: 'fa-solid fa-shirt', done: true },
  { id: 4, title: '为对方做饭', icon: 'fa-solid fa-utensils', done: true },
  { id: 5, title: '海边漫步', icon: 'fa-solid fa-water', done: false },
  { id: 6, title: '拍写真', icon: 'fa-solid fa-camera', done: false },
  { id: 7, title: '看演唱会', icon: 'fa-solid fa-microphone', done: false },
  { id: 8, title: '跨年拥抱', icon: 'fa-solid fa-champagne-glasses', done: true },
  { id: 9, title: '做陶艺', icon: 'fa-solid fa-hands', done: false },
  { id: 10, title: '爬山登顶', icon: 'fa-solid fa-mountain', done: false },
]);

// 日常点滴数据
const articles = ref([
  { title: '第一次一起过中秋节', date: '2023-09-29', desc: '今年的月亮特别圆，我们在楼顶吹着微风，吃着你最爱的流心月饼...', cover: 'https://images.unsplash.com/photo-1537243917822-4a00cb0bdcdd?q=80&w=800' },
  { title: '冬日里的第一场雪', date: '2023-12-15', desc: '南方孩子看到雪的激动，在雪地里写下我们的名字，手冻得通红但心里很暖。', cover: 'https://images.unsplash.com/photo-1483921020237-2ff51e8e4b22?q=80&w=800' },
  { title: '周末的治愈系烘焙', date: '2024-03-10', desc: '烤箱里飘出阵阵黄油香，虽然蛋挞烤得稍微有点焦，但依然是我们心中的米其林三星。', cover: 'https://images.unsplash.com/photo-1509440159596-0249088772ff?q=80&w=800' },
]);

// 回忆相册数据
const photos = ref([
  'https://images.unsplash.com/photo-1516589178581-6cd7833ae3b2?q=80&w=500',
  'https://images.unsplash.com/photo-1522673607200-164d1b6ce486?q=80&w=500',
  'https://images.unsplash.com/photo-1518199266791-5375a83190b7?q=80&w=500',
  'https://images.unsplash.com/photo-1494790108377-be9c29b29330?q=80&w=500',
  'https://images.unsplash.com/photo-1506744626753-1fa28f67c9fe?q=80&w=500',
  'https://images.unsplash.com/photo-1529333166437-7750a6dd5a70?q=80&w=500',
]);

// 祝福留言数据
const comments = ref([
  { name: '小明', time: '2小时前', avatar: 'https://api.dicebear.com/7.x/notionists/svg?seed=Felix', text: '太甜了太甜了！一定要一直幸福下去哦！🎉' },
  { name: '阿花', time: '昨天', avatar: 'https://api.dicebear.com/7.x/notionists/svg?seed=Aneka', text: '神仙眷侣，羡慕这两个字我已经说倦了。' },
  { name: '老王', time: '3天前', avatar: 'https://api.dicebear.com/7.x/notionists/svg?seed=Jack', text: '网站做得真好看，99不88！' },
  { name: '喵喵', time: '5天前', avatar: 'https://api.dicebear.com/7.x/notionists/svg?seed=Mimi', text: '日常催更，想看你们更多的点滴！' },
]);

onMounted(() => {
  autoPlayTimer = setInterval(nextSlide, 5000);
  window.addEventListener('scroll', handleScroll, { passive: true });
  updateTimer();
  countdownInterval = setInterval(updateTimer, 1000);
});

onUnmounted(() => {
  if (autoPlayTimer) clearInterval(autoPlayTimer);
  if (countdownInterval) clearInterval(countdownInterval);
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Noto+Serif+SC:wght@700;900&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css');

/* 防止水平溢出但不创建独立滚动容器 */
.lg-newui-app { overflow-x: clip; }

.font-cursive { font-family: 'Dancing Script', cursive; }
.lg-font-serif { font-family: 'Noto Serif SC', serif; }
.font-chinese { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif; }

/* 标题高亮装饰 */
.lg-title-highlight { position: relative; z-index: 1; display: inline-block; }
.lg-title-highlight::before {
    content: ''; position: absolute; left: -0.2em; right: -0.2em; bottom: 0.1em; height: 0.5em;
    background: linear-gradient(120deg, rgba(253, 224, 71, 0.4) 0%, rgba(250, 204, 21, 0.3) 100%);
    z-index: -1; transform: skewX(-15deg) rotate(-2deg); border-radius: 4px; pointer-events: none;
}

/* 隐藏留言框的滚动条，保持美观 */
.custom-scrollbar::-webkit-scrollbar { width: 4px; }
.custom-scrollbar::-webkit-scrollbar-thumb { background-color: #E5E7EB; border-radius: 10px; }

/* 波浪动画 */
.waves { position: absolute; bottom: 0; left: 0; width: 100%; height: 12vh; min-height: 80px; max-height: 150px; margin-bottom: -7px;}
.parallax > use { animation: move-forever 25s cubic-bezier(.55,.5,.45,.5) infinite; }
.parallax > use:nth-child(1) { animation-delay: -2s; animation-duration: 7s; }
.parallax > use:nth-child(2) { animation-delay: -3s; animation-duration: 10s; }
.parallax > use:nth-child(3) { animation-delay: -4s; animation-duration: 13s; }
.parallax > use:nth-child(4) { animation-delay: -5s; animation-duration: 20s; }
@keyframes move-forever { 0% { transform: translate3d(-90px,0,0); } 100% { transform: translate3d(85px,0,0); } }

/* 吸顶 Header 左右弹入 + 脉冲 */
.sticky-bar-enter-active, .sticky-bar-leave-active { transition: opacity 0.3s ease; }
.sticky-bar-enter-from, .sticky-bar-leave-to { opacity: 0; }
.sticky-bar-enter-active .nav-left { animation: slide-in-left 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) forwards; }
.sticky-bar-enter-active .nav-center { animation: slide-in-up 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) forwards; }
.sticky-bar-enter-active .nav-right { animation: slide-in-right 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) forwards; }
@keyframes slide-in-left { 0% { transform: translateX(-150%) scale(0.9); opacity: 0; } 60% { transform: translateX(5%) scale(1.05); opacity: 1; } 100% { transform: translateX(0) scale(1); opacity: 1; } }
@keyframes slide-in-right { 0% { transform: translateX(150%) scale(0.9); opacity: 0; } 60% { transform: translateX(-5%) scale(1.05); opacity: 1; } 100% { transform: translateX(0) scale(1); opacity: 1; } }
@keyframes slide-in-up { 0% { transform: translateY(-100%) scale(0.9); opacity: 0; } 60% { transform: translateY(10%) scale(1.05); opacity: 1; } 100% { transform: translateY(0) scale(1); opacity: 1; } }

/* 回顶按钮 Fade + Slide 动画 */
.fade-slide-enter-active, .fade-slide-leave-active { transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1); }
.fade-slide-enter-from, .fade-slide-leave-to { opacity: 0; transform: translateY(30px) scale(0.8); }
</style>