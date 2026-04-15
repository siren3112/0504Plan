<template>
  <div class="lg-newui-app font-chinese text-gray-800 bg-[#F8F9FA] min-h-screen relative overflow-x-hidden">
    
    <header class="fixed top-0 left-0 w-full z-50 h-[60px] md:h-[72px] px-4 md:px-6 flex items-center bg-white/80 backdrop-blur-xl border-b border-white/20 shadow-sm transition-none">
      
      <div :class="['w-full h-full flex items-center justify-center transition-none', isScrolled ? 'md:hidden' : '']">
        <h1 class="font-zhimang text-2xl md:text-3xl font-bold text-gray-800 tracking-wider drop-shadow-sm">燕过微风</h1>
        <div class="absolute right-4 md:right-6 w-8 h-8 md:w-10 md:h-10 bg-[#FF6B6B] hover:bg-[#ff5252] text-white rounded-[8px] md:rounded-[10px] shadow-md flex items-center justify-center cursor-pointer transition-colors">
          <i class="fa-solid fa-comment-dots text-sm md:text-base"></i>
        </div>
      </div>

      <div :class="['w-full h-full items-center justify-between hidden transition-none', isScrolled ? 'md:flex' : '']">
        <div class="flex items-center gap-3">
          <div class="bg-black/90 text-white px-4 py-1.5 rounded-full flex items-center gap-2 shadow-md">
            <span class="font-bold text-sm tracking-widest">Ki.</span>
            <div class="flex items-center text-red-500"><i class="fa-solid fa-heart text-xs animate-pulse"></i></div>
            <span class="font-bold text-sm tracking-widest">Really</span>
          </div>
        </div>
        
        <nav v-if="isScrolled" class="absolute left-1/2 top-1/2 flex items-center bg-white/90 backdrop-blur-md rounded-full p-1 md:p-1.5 shadow-sm border border-gray-100 animate-nav-bounce">
          <a v-for="item in navItems" :key="item.name" href="#" @click.prevent="activeMenu = item.name" 
             :class="['px-3 lg:px-5 py-2 rounded-full text-[12px] lg:text-[13px] font-medium transition-colors flex items-center gap-1.5 lg:gap-2 whitespace-nowrap', activeMenu === item.name ? 'bg-red-400 text-white shadow-md shadow-red-200 animate-rubber-band' : 'text-gray-600 hover:bg-gray-100/80']">
             <i :class="item.icon" :style="activeMenu === item.name ? 'font-size: 14px;' : 'font-size: 12px;'"></i>
             <span>{{ item.name }}</span>
          </a>
        </nav>

        <div class="flex items-center gap-4">
           <div class="w-9 h-9 rounded-full overflow-hidden border-2 border-white shadow-sm cursor-pointer hover:scale-110 transition-transform">
             <img src="https://0317.gz.cn/img/she.jpg" class="w-full h-full object-cover">
           </div>
        </div>
      </div>
    </header>

    <section class="relative w-full h-[400px] md:h-[800px] overflow-hidden bg-[#E2E8DF] flex flex-col items-center justify-center mt-[-60px] md:mt-[-72px]">
      
      <div class="absolute inset-0 w-full h-full z-0">
        <div v-for="(img, index) in bannerImages" :key="index" 
             :class="['absolute inset-0 w-full h-full bg-cover bg-center transition-opacity duration-1500 ease-in-out', currentIndex === index ? 'opacity-100' : 'opacity-0']" 
             :style="{ backgroundImage: `url(${img})` }">
        </div>
      </div>

      <div class="relative z-20 w-full h-full pointer-events-none flex justify-center items-center px-4 mt-[60px] md:mt-[72px]">
         <div class="relative w-full max-w-[340px] md:max-w-2xl flex justify-between items-center pointer-events-auto transform scale-[0.8] md:scale-100 origin-center">
            
            <div class="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 flex flex-col items-center gap-3 pointer-events-auto z-30 mt-[-10px] md:mt-0">
               <div class="bg-white/40 backdrop-blur-md px-4 py-1.5 rounded-full flex items-center gap-2 shadow-sm border border-white/40 hover:bg-white/50 transition-colors whitespace-nowrap">
                  <div class="w-5 h-5 rounded-full bg-white/80 flex items-center justify-center">
                     <i class="fa-solid fa-paper-plane text-gray-500 text-[10px]"></i>
                  </div>
                  <span class="text-[13px] font-bold text-gray-800 tracking-wider">相距 12490.7 km</span>
               </div>
               
               <div class="w-14 h-14 md:w-16 md:h-16 hover:scale-110 transition-transform animate-pulse mt-2">
                  <img src="https://loveli.kikiw.cn/Style/img/heart.png" alt="heart" class="w-full h-full object-contain drop-shadow-xl" 
                       onerror="this.src='data:image/svg+xml;utf8,<svg xmlns=\'http://www.w3.org/2000/svg\' viewBox=\'0 0 512 512\'><path fill=\'%23FF4D4F\' d=\'M462.3 62.6C407.5 15.9 326 24.3 275.7 76.2L256 96.5l-19.7-20.3C186.1 24.3 104.5 15.9 49.7 62.6c-62.8 53.6-66.1 149.8-9.9 207.9l193.5 199.8c12.5 12.9 32.8 12.9 45.3 0l193.5-199.8c56.3-58.1 53-154.3-9.8-207.9z\'/></svg>'">
               </div>
            </div>

            <div class="relative flex flex-col items-center">
               <div class="w-[120px] h-[120px] md:w-[150px] md:h-[150px] relative pointer-events-auto rounded-full border-4 border-white/40 shadow-lg overflow-hidden transition-transform duration-300 hover:scale-105">
                  <img src="https://0317.gz.cn/img/she.jpg" class="absolute inset-0 w-full h-full object-cover" alt="Ki.">
               </div>
               <div class="mt-[-15px] bg-black/60 backdrop-blur-sm text-white/90 px-6 py-1.5 rounded-full text-[11px] font-bold shadow-md tracking-widest cursor-pointer hover:bg-black/80 transition-colors z-10">Ki.</div>
            </div>
            
            <div class="relative flex flex-col items-center">
               <div class="w-[120px] h-[120px] md:w-[150px] md:h-[150px] relative pointer-events-auto rounded-full border-4 border-white/40 shadow-lg overflow-hidden transition-transform duration-300 hover:scale-105">
                  <img src="https://0317.gz.cn/img/he.jpg" class="absolute inset-0 w-full h-full object-cover" alt="Really">
               </div>
               <div class="mt-[-15px] bg-black/60 backdrop-blur-sm text-white/90 px-6 py-1.5 rounded-full text-[11px] font-bold shadow-md tracking-widest cursor-pointer hover:bg-black/80 transition-colors z-10">Really</div>
            </div>
         </div>
      </div>

      <div class="absolute bottom-0 left-0 w-full z-10 leading-none">
        <svg class="waves block w-full h-[15px] md:h-[100px]" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 24 150 28" preserveAspectRatio="none" shape-rendering="auto">
          <defs><path id="gentle-wave" d="M-160 44c30 0 58-18 88-18s 58 18 88 18 58-18 88-18 58 18 88 18 v44h-352z" /></defs>
          <g class="parallax">
            <use xlink:href="#gentle-wave" x="48" y="0" fill="rgba(255, 255, 255, 0.3)" />
            <use xlink:href="#gentle-wave" x="48" y="3" fill="rgba(255, 255, 255, 0.5)" />
            <use xlink:href="#gentle-wave" x="48" y="5" fill="rgba(255, 255, 255, 0.7)" />
            <use xlink:href="#gentle-wave" x="48" y="7" fill="#FFFFFF" />
          </g>
        </svg>
      </div>
    </section>

    <div ref="originalMenuRef" class="w-full bg-white relative z-20 pt-4 md:pt-6 pb-10 md:pb-12">
       <nav :class="['hidden md:flex items-center justify-center gap-8 px-6 w-full text-[13px] font-medium text-gray-500 pb-2 transition-none', isScrolled ? 'opacity-0 pointer-events-none' : 'opacity-100']">
          <a v-for="item in navItems" :key="item.name" href="#" @click.prevent="activeMenu = item.name" class="group flex items-center gap-2 transition-colors hover:text-gray-900">
             
             <div v-if="activeMenu === item.name" class="flex items-center justify-center rounded-full w-11 h-11 bg-[#FF6B6B] text-white shadow-md shadow-red-200 animate-rubber-band">
                <i :class="item.icon" class="text-base"></i>
             </div>
             
             <template v-else>
                <i :class="item.icon" class="text-xs transition-transform group-hover:scale-110"></i>
                <span class="tracking-wide whitespace-nowrap">{{ item.name }}</span>
             </template>
          </a>
       </nav>
       
       <div class="text-center mt-6 md:mt-10">
          <div class="flex items-center justify-center gap-2 text-gray-400 font-cursive text-xs md:text-sm mb-2">
             <i class="fa-solid fa-asterisk text-[8px] md:text-[10px] text-gray-300"></i>
             <span>Our Cozy Place</span>
             <i class="fa-solid fa-asterisk text-[8px] md:text-[10px] text-gray-300"></i>
          </div>
          <h2 class="text-xl md:text-3xl font-bold text-gray-800 tracking-widest lg-font-serif">收好我们的日常与心动</h2>
       </div>
    </div>


    <main class="w-full max-w-[1100px] mx-auto px-4 pb-28 md:pb-20 relative z-30 pt-10 space-y-16 md:space-y-20">
       
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
                 <Transition name="num-tick" mode="out-in">
                    <span :key="displayTimer.days" class="text-7xl md:text-[100px] lg:text-[120px] leading-[0.85] font-black text-[#2A303C] tracking-tighter tabular-nums drop-shadow-sm inline-block">{{ displayTimer.days }}</span>
                 </Transition>
                 <div class="w-8 h-[4px] bg-[#FA5252] mt-6 md:mt-8 mb-3 rounded-full opacity-90"></div>
                 <span class="text-[10px] text-[#FA5252] tracking-[0.3em] font-bold">DAYS</span>
               </div>
               
               <div class="flex gap-8 text-[#2A303C]">
                 <div class="flex flex-col items-center w-12">
                    <Transition name="num-tick" mode="out-in">
                      <span :key="displayTimer.hours" class="text-[26px] font-bold leading-none tabular-nums inline-block">{{ displayTimer.hours }}</span>
                    </Transition>
                    <span class="text-[9px] text-gray-400 tracking-[0.15em] mt-2 font-medium">HOURS</span>
                 </div>
                 <div class="flex flex-col items-center w-12">
                    <Transition name="num-tick" mode="out-in">
                       <span :key="displayTimer.minutes" class="text-[26px] font-bold leading-none tabular-nums inline-block">{{ displayTimer.minutes }}</span>
                    </Transition>
                    <span class="text-[9px] text-gray-400 tracking-[0.15em] mt-2 font-medium">MINUTES</span>
                 </div>
                 <div class="flex flex-col items-center w-12">
                    <Transition name="num-tick" mode="out-in">
                       <span :key="displayTimer.seconds" class="text-[26px] font-bold leading-none tabular-nums inline-block text-[#FF6B6B]">{{ displayTimer.seconds }}</span>
                    </Transition>
                    <span class="text-[9px] text-[#FF6B6B] tracking-[0.15em] mt-2 font-medium">SECONDS</span>
                 </div>
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
             <article v-for="(article, index) in articles" :key="index" v-slide-up :style="{ transitionDelay: `${index * 150}ms` }" class="bg-white rounded-[24px] overflow-hidden shadow-[0_8px_30px_rgb(0,0,0,0.04)] hover:shadow-[0_15px_40px_rgb(0,0,0,0.08)] transition-all duration-500 hover:-translate-y-2 cursor-pointer group">
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
             <div v-for="(photo, index) in photos" :key="index" v-slide-up :style="{ transitionDelay: `${(index % 4) * 100}ms` }" class="relative break-inside-avoid rounded-[16px] overflow-hidden group cursor-zoom-in shadow-sm hover:shadow-lg transition-all">
                <img :src="photo" class="w-full h-auto object-cover transition-transform duration-700 group-hover:scale-110" loading="lazy">
                <div class="absolute inset-0 bg-black/0 group-hover:bg-black/20 transition-colors duration-300 flex items-center justify-center">
                   <i class="fa-solid fa-magnifying-glass-plus text-white text-3xl opacity-0 group-hover:opacity-100 transition-all duration-300 transform scale-50 group-hover:scale-100"></i>
                </div>
             </div>
          </div>
       </section>

    </main>

    <footer class="bg-white border-t border-gray-100 mt-20 py-12" v-slide-up>
       <div class="max-w-[1100px] mx-auto px-4 flex flex-col items-center justify-center text-center pb-20 md:pb-0">
          <div class="flex items-center gap-2 text-3xl font-bold mb-4 font-zhimang text-gray-800">
             <span>燕过</span>
             <i class="fa-solid fa-heart text-rose-500 animate-pulse text-sm mx-1"></i>
             <span>微风</span>
          </div>
          <p class="text-xs text-gray-500 mb-3 tracking-widest">收好我们的日常与心动</p>
          <div class="flex flex-wrap items-center justify-center gap-4 text-[11px] text-gray-400 mt-2 font-medium">
             <span>© 2024 Our Cozy Place.</span>
             <a href="#" class="hover:text-gray-700 transition-colors">萌ICP备20230000号</a>
             <span class="bg-gray-100 px-2 py-1 rounded">已平稳运行 {{ displayTimer.days }} 天</span>
          </div>
       </div>
    </footer>

    <nav class="fixed bottom-6 left-1/2 -translate-x-1/2 w-max min-w-[280px] bg-white/70 backdrop-blur-2xl border border-white/50 z-[100] flex md:hidden items-center justify-evenly px-4 py-3 rounded-[2rem] shadow-[0_10px_40px_rgba(0,0,0,0.1)]">
       <a v-for="item in navItems" :key="item.name" href="#" @click.prevent="activeMenu = item.name" class="group flex flex-col items-center mx-2 md:mx-3 transition-colors text-gray-500 hover:text-[#FF6B6B]">
           <div v-if="activeMenu === item.name" class="flex items-center justify-center rounded-full w-12 h-12 bg-[#FF6B6B] text-white shadow-md shadow-red-200 transform -translate-y-4 border-[4px] border-[#F8F9FA]/80 animate-rubber-band">
               <i :class="item.icon" class="text-[20px]"></i>
           </div>
           <div v-else class="flex items-center justify-center w-8 h-8 transition-transform duration-300 hover:scale-110">
               <i :class="item.icon" class="text-[18px]"></i>
           </div>
       </a>
    </nav>

    <Transition name="fade-slide">
      <button v-show="showBackToTop" @click="scrollToTop" class="fixed bottom-24 md:bottom-10 right-6 md:right-10 w-11 h-11 md:w-12 md:h-12 bg-blue-500 text-white rounded-full flex items-center justify-center shadow-[0_5px_20px_rgba(59,130,246,0.4)] hover:bg-blue-600 transition-all duration-300 z-50 group hover:-translate-y-2 cursor-pointer border-2 border-white" title="回到顶部">
        <i class="fa-solid fa-arrow-up text-base md:text-lg group-hover:animate-bounce"></i>
      </button>
    </Transition>

  </div>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue';

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

const isScrolled = ref(false);
const showBackToTop = ref(false);
const originalMenuRef = ref(null);

// 🌟 选中的活动菜单状态
const activeMenu = ref('首页');

const navItems = [
  { name: '点滴', icon: 'fa-solid fa-droplet' },
  { name: '留言', icon: 'fa-solid fa-message' },
  { name: '轨迹', icon: 'fa-solid fa-shoe-prints' },
  { name: '首页', icon: 'fa-solid fa-house' },
  { name: '相册', icon: 'fa-solid fa-camera-retro' },
  { name: '清单', icon: 'fa-solid fa-list-check' },
  { name: '关于', icon: 'fa-solid fa-circle-info' }
];

const bannerImages = ref([
  'https://loveli.kikiw.cn/Style/img/bg.jpg', 
  'https://images.unsplash.com/photo-1473448912268-2022ce9509d8?q=80&w=2000&auto=format&fit=crop'
]);
const currentIndex = ref(0);
let autoPlayTimer = null;
const setSlide = (index) => { currentIndex.value = index; };
const nextSlide = () => { currentIndex.value = (currentIndex.value + 1) % bannerImages.value.length; };

const scrollToTop = () => { window.scrollTo({ top: 0, behavior: 'smooth' }); };

const handleScroll = () => {
  const scrollY = window.scrollY;
  if (originalMenuRef.value) {
    const rect = originalMenuRef.value.getBoundingClientRect();
    const headerHeight = window.innerWidth >= 768 ? 72 : 60;
    isScrolled.value = rect.top <= headerHeight;
  }
  showBackToTop.value = scrollY > 600;
};

// 🌟 计时器：使用 displayTimer 驱动界面更新
const startDate = new Date('2023-07-19T00:00:00').getTime();
const displayTimer = reactive({ days: 0, hours: '00', minutes: '00', seconds: '00' });
let countdownInterval = null;

const padZero = (num) => (num < 10 ? `0${num}` : num);

// 🌟 页面初次加载时极速数字翻滚动画核心方法
const animateValue = (obj, key, start, end, duration) => {
  let startTimestamp = null;
  const easeOutExpo = (t) => t === 1 ? 1 : 1 - Math.pow(2, -10 * t);
  const step = (timestamp) => {
    if (!startTimestamp) startTimestamp = timestamp;
    const progress = Math.min((timestamp - startTimestamp) / duration, 1);
    const current = Math.floor(start + (end - start) * easeOutExpo(progress));
    obj[key] = key === 'days' ? current : padZero(current);
    
    if (progress < 1) window.requestAnimationFrame(step);
    else obj[key] = key === 'days' ? end : padZero(end);
  };
  window.requestAnimationFrame(step);
};

// 启动时间系统
const initTimer = () => {
  const distance = Math.max(0, new Date().getTime() - startDate);
  const tDays = Math.floor(distance / (1000 * 60 * 60 * 24));
  const tHours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  const tMins = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
  const tSecs = Math.floor((distance % (1000 * 60)) / 1000);

  // 炫酷入场动画
  animateValue(displayTimer, 'days', 0, tDays, 2000);
  animateValue(displayTimer, 'hours', 0, tHours, 1500);
  animateValue(displayTimer, 'minutes', 0, tMins, 1500);
  animateValue(displayTimer, 'seconds', 0, tSecs, 1500);

  // 动画完毕后无缝接管常规跳动
  setTimeout(() => {
    countdownInterval = setInterval(() => {
      const d = Math.max(0, new Date().getTime() - startDate);
      displayTimer.days = Math.floor(d / (1000 * 60 * 60 * 24));
      displayTimer.hours = padZero(Math.floor((d % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)));
      displayTimer.minutes = padZero(Math.floor((d % (1000 * 60 * 60)) / (1000 * 60)));
      displayTimer.seconds = padZero(Math.floor((d % (1000 * 60)) / 1000));
    }, 1000);
  }, 2000);
};

const statsCards = ref([
  { id: 1, title: '恋爱天气', subtitle: '深圳', value: '28°', bg: 'bg-gradient-to-br from-blue-400 to-blue-500', icon: 'fa-solid fa-cloud-sun' },
  { id: 2, title: '恋爱天气', subtitle: '东莞', value: '26°', bg: 'bg-gradient-to-br from-orange-400 to-orange-500', icon: 'fa-solid fa-sun' },
  { id: 3, title: '完成约定', subtitle: 'Love List', value: '17/29', bg: 'bg-[#7D8592] md:col-span-2', icon: 'fa-solid fa-list-check' },
]);
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
const articles = ref([
  { title: '第一次一起过中秋节', date: '2023-09-29', desc: '今年的月亮特别圆，我们在楼顶吹着微风，吃着你最爱的流心月饼...', cover: 'https://images.unsplash.com/photo-1537243917822-4a00cb0bdcdd?q=80&w=800' },
  { title: '冬日里的第一场雪', date: '2023-12-15', desc: '南方孩子看到雪的激动，在雪地里写下我们的名字，手冻得通红但心里很暖。', cover: 'https://images.unsplash.com/photo-1483921020237-2ff51e8e4b22?q=80&w=800' },
  { title: '周末的治愈系烘焙', date: '2024-03-10', desc: '烤箱里飘出阵阵黄油香，虽然蛋挞烤得稍微有点焦，但依然是我们心中的米其林三星。', cover: 'https://images.unsplash.com/photo-1509440159596-0249088772ff?q=80&w=800' },
]);
const photos = ref([
  'https://images.unsplash.com/photo-1516589178581-6cd7833ae3b2?q=80&w=500',
  'https://images.unsplash.com/photo-1522673607200-164d1b6ce486?q=80&w=500',
  'https://images.unsplash.com/photo-1518199266791-5375a83190b7?q=80&w=500',
  'https://images.unsplash.com/photo-1494790108377-be9c29b29330?q=80&w=500',
  'https://images.unsplash.com/photo-1506744626753-1fa28f67c9fe?q=80&w=500',
  'https://images.unsplash.com/photo-1529333166437-7750a6dd5a70?q=80&w=500',
]);
const comments = ref([
  { name: '小明', time: '2小时前', avatar: 'https://api.dicebear.com/7.x/notionists/svg?seed=Felix', text: '太甜了太甜了！一定要一直幸福下去哦！🎉' },
  { name: '阿花', time: '昨天', avatar: 'https://api.dicebear.com/7.x/notionists/svg?seed=Aneka', text: '神仙眷侣，羡慕这两个字我已经说倦了。' },
  { name: '老王', time: '3天前', avatar: 'https://api.dicebear.com/7.x/notionists/svg?seed=Jack', text: '网站做得真好看，99不88！' },
  { name: '喵喵', time: '5天前', avatar: 'https://api.dicebear.com/7.x/notionists/svg?seed=Mimi', text: '日常催更，想看你们更多的点滴！' },
]);

onMounted(() => {
  autoPlayTimer = setInterval(nextSlide, 5000);
  window.addEventListener('scroll', handleScroll, { passive: true });
  initTimer();
});

onUnmounted(() => {
  if (autoPlayTimer) clearInterval(autoPlayTimer);
  if (countdownInterval) clearInterval(countdownInterval);
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Zhi+Mang+Xing&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Noto+Serif+SC:wght@700;900&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css');

.lg-newui-app { overflow-x: clip; }
.font-zhimang { font-family: 'Zhi Mang Xing', cursive; }
.font-cursive { font-family: 'Dancing Script', cursive; }
.lg-font-serif { font-family: 'Noto Serif SC', serif; }
.font-chinese { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif; }

.custom-scrollbar::-webkit-scrollbar { width: 4px; }
.custom-scrollbar::-webkit-scrollbar-thumb { background-color: #E5E7EB; border-radius: 10px; }

.hide-scrollbar::-webkit-scrollbar { display: none; }
.hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

/* tabular-nums: 等宽数字渲染，有效防止计时器宽度发生闪烁 */
.tabular-nums { font-variant-numeric: tabular-nums; }

/* 🌟 Vue 3 时间数字垂直翻滚切入切出动效 */
.num-tick-enter-active, .num-tick-leave-active {
  transition: all 0.15s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}
.num-tick-enter-from {
  opacity: 0;
  transform: translateY(15px) scale(0.9);
}
.num-tick-leave-to {
  opacity: 0;
  transform: translateY(-15px) scale(0.9);
}

/* 波浪动画：移动端扁平化为 15px */
.waves { position: absolute; bottom: 0; left: 0; width: 100%; height: 12vh; min-height: 80px; max-height: 150px; margin-bottom: -7px;}
.parallax > use { animation: move-forever 25s cubic-bezier(.55,.5,.45,.5) infinite; }
.parallax > use:nth-child(1) { animation-delay: -2s; animation-duration: 7s; }
.parallax > use:nth-child(2) { animation-delay: -3s; animation-duration: 10s; }
.parallax > use:nth-child(3) { animation-delay: -4s; animation-duration: 13s; }
.parallax > use:nth-child(4) { animation-delay: -5s; animation-duration: 20s; }
@keyframes move-forever { 0% { transform: translate3d(-90px,0,0); } 100% { transform: translate3d(85px,0,0); } }

/* 菜单整体弹跳出现 */
@keyframes navBounceIn {
  0% { opacity: 0; transform: translate(-50%, -50%) scale3d(0.3, 0.3, 0.3); }
  20% { transform: translate(-50%, -50%) scale3d(1.1, 1.1, 1.1); }
  40% { transform: translate(-50%, -50%) scale3d(0.9, 0.9, 0.9); }
  60% { opacity: 1; transform: translate(-50%, -50%) scale3d(1.03, 1.03, 1.03); }
  80% { transform: translate(-50%, -50%) scale3d(0.97, 0.97, 0.97); }
  100% { opacity: 1; transform: translate(-50%, -50%) scale3d(1, 1, 1); }
}
.animate-nav-bounce { animation: navBounceIn 0.75s cubic-bezier(0.215, 0.61, 0.355, 1) both; }

/* 点击菜单项的橡皮筋拉伸效果 */
@keyframes rubberBandEffect {
  0% { transform: scale3d(1, 1, 1); }
  30% { transform: scale3d(1.25, 0.75, 1); }
  40% { transform: scale3d(0.75, 1.25, 1); }
  50% { transform: scale3d(1.15, 0.85, 1); }
  65% { transform: scale3d(0.95, 1.05, 1); }
  75% { transform: scale3d(1.05, 0.95, 1); }
  100% { transform: scale3d(1, 1, 1); }
}
.animate-rubber-band {
  animation: rubberBandEffect 0.8s ease both;
}

.fade-slide-enter-active, .fade-slide-leave-active { transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1); }
.fade-slide-enter-from, .fade-slide-leave-to { opacity: 0; transform: translateY(30px) scale(0.8); }
</style>