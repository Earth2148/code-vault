<!DOCTYPE html>
<html lang="th" class="h-full bg-black">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>CodeVault - Dark Skeuomorphic Media Manager</title>

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
  <!-- Vue.js 3 CDN -->
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

  <!-- PWA Manifest & Service Worker Link -->
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#ea580c">
  <link rel="apple-touch-icon" href="https://placehold.co/192x192/ea580c/ffffff?text=VAULT">

  <script>
    /* Register Service Worker for PWA Offline Support */
    if ('serviceWorker' in navigator) {
      window.addEventListener('load', () => {
        navigator.serviceWorker.register('sw.js').catch(err => console.log('SW registration failed:', err));
      });
    }

    tailwind.config = {
      theme: {
        extend: {
          colors: {
            brand: {
              black: '#0d0e11',
              dark: '#14161b',
              card: '#1a1d24',
              orange: '#f97316',
              orangeDark: '#ea580c',
              orangeGlow: '#ff8c00',
              gray: '#8a94a6'
            }
          },
          boxShadow: {
            // Skeuomorphic & Dark Neumorphic depth shadows
            'skeuo-raised': '6px 6px 14px #090a0c, -6px -6px 14px #232730',
            'skeuo-raised-sm': '3px 3px 8px #08090a, -3px -3px 8px #22262f',
            'skeuo-inset': 'inset 4px 4px 8px #08090a, inset -4px -4px 8px #22262f',
            'skeuo-inset-sm': 'inset 2px 2px 4px #070809, inset -2px -2px 4px #20242c',
            'orange-glow': '0 0 15px rgba(249, 115, 22, 0.5), 4px 4px 10px #090a0c',
            'orange-glow-sm': '0 0 8px rgba(249, 115, 22, 0.4)'
          }
        }
      }
    }
  </script>

  <style>
    @import url('https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&family=JetBrains+Mono:wght@500;700&display=swap');
    
    * {
      touch-action: manipulation;
      user-select: none;
    }
    body {
      font-family: 'Kanit', sans-serif;
      background-color: #070809;
      color: #e2e8f0;
      -webkit-tap-highlight-color: transparent;
    }
    .font-code {
      font-family: 'JetBrains Mono', monospace;
    }

    /* Skeuomorphic Glossy Metallic Buttons */
    .btn-orange-skeuo {
      background: linear-gradient(145deg, #ff8c00, #ea580c);
      box-shadow: 4px 4px 10px #08090a, -2px -2px 6px rgba(255, 255, 255, 0.15), inset 0 1px 1px rgba(255, 255, 255, 0.4);
      color: #ffffff;
      transition: all 0.15s ease;
    }
    .btn-orange-skeuo:active {
      background: linear-gradient(145deg, #d97706, #c2410c);
      box-shadow: inset 3px 3px 6px rgba(0,0,0,0.6), inset -2px -2px 4px rgba(255,255,255,0.2);
      transform: translateY(1px);
    }

    .btn-dark-skeuo {
      background: linear-gradient(145deg, #1f232b, #15171d);
      box-shadow: 5px 5px 12px #090a0c, -4px -4px 10px #232731, inset 0 1px 1px rgba(255,255,255,0.1);
      transition: all 0.15s ease;
    }
    .btn-dark-skeuo:active {
      box-shadow: inset 3px 3px 6px #08090a, inset -3px -3px 6px #232731;
      transform: translateY(1px);
    }

    /* Blur & Image transition */
    .img-blur-hidden {
      filter: blur(20px) brightness(0.6) contrast(1.2);
      transform: scale(1.15);
      transition: filter 0.4s cubic-bezier(0.4, 0, 0.2, 1), transform 0.4s ease;
    }
    .img-blur-visible {
      filter: blur(0px) brightness(1) contrast(1);
      transform: scale(1);
      transition: filter 0.4s cubic-bezier(0.4, 0, 0.2, 1), transform 0.4s ease;
    }

    /* Custom Scrollbars */
    ::-webkit-scrollbar { width: 4px; height: 4px; }
    ::-webkit-scrollbar-track { background: #0d0e11; }
    ::-webkit-scrollbar-thumb { background: #2d333f; border-radius: 99px; }
    ::-webkit-scrollbar-thumb:hover { background: #ea580c; }
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
  </style>
</head>
<body class="h-full select-none overflow-x-hidden antialiased bg-black flex justify-center">

  <div id="app" class="w-full max-w-md min-h-screen bg-brand-black text-slate-200 flex flex-col relative border-x border-slate-900 shadow-2xl">

    <!-- PIN LOCK OVERLAY -->
    <div v-if="isLocked" class="fixed inset-0 z-50 bg-brand-black flex flex-col items-center justify-center p-6 text-center max-w-md mx-auto border-x border-slate-900">
      
      <!-- Skeuomorphic Key Lock Badge -->
      <div class="w-24 h-24 rounded-3xl bg-brand-dark shadow-skeuo-raised flex items-center justify-center mb-6 relative border border-slate-800/80">
        <div class="w-16 h-16 rounded-2xl bg-brand-black shadow-skeuo-inset flex items-center justify-center text-brand-orange border border-orange-500/20">
          <i class="fa-solid fa-shield-halved text-3xl animate-pulse"></i>
        </div>
      </div>
      
      <h2 class="text-2xl font-bold text-white tracking-wider font-code mb-1">CODEVAULT</h2>
      <p class="text-brand-gray text-xs mb-8">กรอกรหัส PIN 4 หลักเพื่อเข้าใช้งานส่วนตัว</p>

      <!-- PIN Dots -->
      <div class="flex gap-5 mb-10">
        <div v-for="n in 4" :key="n" 
             class="w-4 h-4 rounded-full transition-all duration-300 border border-slate-800"
             :class="pinInput.length >= n ? 'bg-brand-orange shadow-orange-glow border-orange-400' : 'bg-brand-black shadow-skeuo-inset'">
        </div>
      </div>

      <!-- Skeuomorphic Keypad Grid -->
      <div class="grid grid-cols-3 gap-5 w-72 max-w-full mb-6">
        <button v-for="num in [1, 2, 3, 4, 5, 6, 7, 8, 9]" :key="num" @click="appendPin(num)"
                class="w-16 h-16 mx-auto rounded-2xl btn-dark-skeuo text-xl font-bold text-slate-200 flex items-center justify-center border border-slate-800/50">
          {{ num }}
        </button>
        <button @click="clearPin" class="w-16 h-16 mx-auto rounded-2xl btn-dark-skeuo text-slate-400 flex items-center justify-center border border-slate-800/50">
          <i class="fa-solid fa-arrow-rotate-left"></i>
        </button>
        <button @click="appendPin(0)" class="w-16 h-16 mx-auto rounded-2xl btn-dark-skeuo text-xl font-bold text-slate-200 flex items-center justify-center border border-slate-800/50">
          0
        </button>
        <button @click="deletePin" class="w-16 h-16 mx-auto rounded-2xl btn-dark-skeuo text-slate-400 flex items-center justify-center border border-slate-800/50">
          <i class="fa-solid fa-delete-left"></i>
        </button>
      </div>
      
      <p v-if="pinError" class="text-rose-500 text-xs animate-bounce font-medium mt-2">
        <i class="fa-solid fa-circle-exclamation mr-1"></i> รหัส PIN ไม่ถูกต้อง
      </p>
    </div>

    <!-- MAIN CONTENT AREA -->
    <template v-else>

      <!-- TOP NAVIGATION BAR -->
      <header class="sticky top-0 z-30 bg-brand-black/90 backdrop-blur-md px-4 pt-4 pb-2 border-b border-slate-800/60">
        
        <div class="flex items-center justify-between mb-3">
          <!-- Logo -->
          <div class="flex items-center space-x-2.5">
            <div class="w-9 h-9 rounded-xl bg-brand-dark shadow-skeuo-raised flex items-center justify-center text-brand-orange border border-orange-500/30">
              <i class="fa-solid fa-film text-sm"></i>
            </div>
            <div>
              <h1 class="text-lg font-bold text-white tracking-wide font-code flex items-center gap-1.5">
                CODE<span class="text-brand-orange">VAULT</span>
              </h1>
            </div>
          </div>
          
          <!-- Top Controls -->
          <div class="flex items-center space-x-3">
            
            <!-- Global Blur Toggle Switch -->
            <button @click="globalBlurMode = !globalBlurMode" 
                    title="เปิด/ปิดการเบลอรูปภาพทั้งหมด"
                    class="flex items-center gap-1.5 px-3 py-1.5 rounded-xl btn-dark-skeuo text-xs border border-slate-800">
              <i :class="globalBlurMode ? 'fa-solid fa-eye-slash text-brand-orange' : 'fa-solid fa-eye text-emerald-400'"></i>
              <span class="text-[11px] font-medium text-slate-300">{{ globalBlurMode ? 'เบลอรูป' : 'แสดงรูป' }}</span>
            </button>

            <!-- Lock App -->
            <button @click="lockApp" title="ล็อคแอปพลิเคชัน" class="w-9 h-9 rounded-xl btn-dark-skeuo text-slate-400 hover:text-brand-orange flex items-center justify-center border border-slate-800">
              <i class="fa-solid fa-lock text-xs"></i>
            </button>
          </div>
        </div>

        <!-- Skeuomorphic Inset Search Box -->
        <div class="relative mb-3">
          <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-500 text-xs"></i>
          <input type="text" v-model="searchQuery" placeholder="ค้นหารหัส เช่น IPX-888, ชื่อดารา, หมวดหมู่..." 
                 class="w-full bg-brand-black shadow-skeuo-inset text-slate-100 pl-9 pr-9 py-2.5 rounded-xl text-xs outline-none border border-slate-800/80 focus:border-brand-orange/60 transition-all placeholder-slate-600">
          <button v-if="searchQuery" @click="searchQuery = ''" class="absolute right-3 top-1/2 -translate-y-1/2 text-slate-500 hover:text-white w-5 h-5 rounded-full flex items-center justify-center">
            <i class="fa-solid fa-xmark text-xs"></i>
          </button>
        </div>

        <!-- Filter Pill Tabs -->
        <div class="flex items-center gap-2 overflow-x-auto pb-1 no-scrollbar text-[11px] font-medium">
          <button @click="activeStatusFilter = 'ALL'" 
                  :class="activeStatusFilter === 'ALL' ? 'btn-orange-skeuo font-bold' : 'btn-dark-skeuo text-slate-400'"
                  class="px-3.5 py-1.5 rounded-xl whitespace-nowrap border border-slate-800">
            ทั้งหมด ({{ items.length }})
          </button>
          <button @click="activeStatusFilter = 'FAVORITE'" 
                  :class="activeStatusFilter === 'FAVORITE' ? 'btn-orange-skeuo font-bold' : 'btn-dark-skeuo text-slate-400'"
                  class="px-3.5 py-1.5 rounded-xl whitespace-nowrap border border-slate-800 flex items-center gap-1">
            <i class="fa-solid fa-heart text-rose-500"></i> รายการโปรด
          </button>
          <button @click="activeStatusFilter = 'WATCHED'" 
                  :class="activeStatusFilter === 'WATCHED' ? 'btn-orange-skeuo font-bold' : 'btn-dark-skeuo text-slate-400'"
                  class="px-3.5 py-1.5 rounded-xl whitespace-nowrap border border-slate-800 flex items-center gap-1">
            <i class="fa-solid fa-check text-emerald-400"></i> ดูแล้ว
          </button>
          <button @click="activeStatusFilter = 'PLAN'" 
                  :class="activeStatusFilter === 'PLAN' ? 'btn-orange-skeuo font-bold' : 'btn-dark-skeuo text-slate-400'"
                  class="px-3.5 py-1.5 rounded-xl whitespace-nowrap border border-slate-800 flex items-center gap-1">
            <i class="fa-solid fa-clock text-amber-400"></i> รอรับชม
          </button>
        </div>
      </header>

      <!-- MAIN BODY CONTENT -->
      <main class="flex-1 overflow-y-auto px-4 pt-3 pb-28">

        <!-- TAB 1: CODE LIBRARY -->
        <div v-if="activeTab === 'library'" class="space-y-4">
          
          <!-- Bar Info -->
          <div class="flex items-center justify-between text-xs text-slate-400 px-1">
            <span>พบ {{ filteredItems.length }} รายการ</span>
            <div class="flex items-center gap-1.5">
              <span class="text-[10px] text-slate-500">เรียงตาม:</span>
              <select v-model="sortBy" class="bg-brand-dark text-slate-300 rounded-lg px-2 py-1 outline-none text-[11px] border border-slate-800">
                <option value="newest">ล่าสุด</option>
                <option value="code">รหัส (A-Z)</option>
                <option value="rating">คะแนนดาว</option>
              </select>
            </div>
          </div>

          <!-- Empty State -->
          <div v-if="filteredItems.length === 0" class="text-center py-16 px-4">
            <div class="w-16 h-16 rounded-2xl bg-brand-dark shadow-skeuo-inset flex items-center justify-center mx-auto mb-4 text-slate-600 border border-slate-800">
              <i class="fa-solid fa-film text-2xl"></i>
            </div>
            <h3 class="text-slate-300 font-bold mb-1 text-sm">ไม่พบรหัสหนัง</h3>
            <p class="text-xs text-slate-500 mb-5">ลองค้นหาด้วยคำอื่น หรือเพิ่มรหัสใหม่ลงในคลัง</p>
            <button @click="activeTab = 'add'" class="btn-orange-skeuo px-5 py-2.5 rounded-xl text-xs font-bold">
              + เพิ่มรหัสใหม่
            </button>
          </div>

          <!-- Video Code Cards -->
          <div v-else class="space-y-4">
            <div v-for="item in filteredItems" :key="item.id" 
                 class="bg-brand-card shadow-skeuo-raised rounded-2xl p-3.5 border border-slate-800/80 relative overflow-hidden flex flex-col gap-3">
              
              <!-- IMAGE PREVIEW CONTAINER WITH BLUR TOGGLE -->
              <div class="relative w-full h-44 rounded-xl shadow-skeuo-inset overflow-hidden bg-slate-900 border border-slate-800/90 group">
                
                <!-- Image element with dynamic blur class -->
                <img :src="item.imageUrl || getFallbackImage(item.code)" 
                     :class="(globalBlurMode || item.isBlur) ? 'img-blur-hidden' : 'img-blur-visible'"
                     class="w-full h-full object-cover" 
                     @error="handleImgError($event, item.code)" alt="AV Cover">

                <!-- Tap overlay to reveal/hide image -->
                <div @click="toggleItemBlur(item)" class="absolute inset-0 cursor-pointer flex items-center justify-center bg-black/20 hover:bg-black/10 transition">
                  <!-- Eye badge overlay when blurred -->
                  <div v-if="globalBlurMode || item.isBlur" 
                       class="px-3 py-1.5 rounded-full bg-black/70 backdrop-blur-md border border-white/20 text-white text-xs font-medium flex items-center gap-1.5 shadow-lg">
                    <i class="fa-solid fa-eye text-brand-orange"></i>
                    <span>แตะเพื่อปลดล็อกรูป</span>
                  </div>
                </div>

                <!-- Top Badges -->
                <div class="absolute top-2.5 left-2.5 pointer-events-none">
                  <span class="px-2.5 py-1 text-[10px] font-bold font-code bg-black/80 backdrop-blur-md text-brand-orange border border-brand-orange/40 rounded-lg uppercase tracking-wider">
                    {{ item.studio || 'GENERAL' }}
                  </span>
                </div>

                <!-- Favorite Toggle Button -->
                <button @click.stop="toggleFavorite(item)" 
                        class="absolute top-2.5 right-2.5 w-8 h-8 rounded-xl bg-black/70 backdrop-blur-md border border-white/20 flex items-center justify-center text-rose-500 shadow-md active:scale-95 transition">
                  <i :class="item.isFavorite ? 'fa-solid fa-heart text-rose-500' : 'fa-regular fa-heart text-slate-400'"></i>
                </button>

                <!-- Status Badge -->
                <div class="absolute bottom-2.5 right-2.5 pointer-events-none">
                  <span :class="item.status === 'WATCHED' ? 'bg-emerald-950/80 text-emerald-400 border-emerald-500/40' : 'bg-amber-950/80 text-amber-400 border-amber-500/40'" 
                        class="text-[10px] px-2.5 py-0.5 rounded-md font-bold border backdrop-blur-md">
                    {{ item.status === 'WATCHED' ? 'ดูแล้ว' : 'รอรับชม' }}
                  </span>
                </div>

                <!-- Quick Individual Blur Control Icon -->
                <button @click.stop="toggleItemBlur(item)" 
                        class="absolute bottom-2.5 left-2.5 w-7 h-7 rounded-lg bg-black/70 backdrop-blur-md text-slate-300 flex items-center justify-center text-xs border border-white/10">
                  <i :class="(globalBlurMode || item.isBlur) ? 'fa-solid fa-eye-slash' : 'fa-solid fa-eye'"></i>
                </button>
              </div>

              <!-- Content Info -->
              <div class="px-1 space-y-2">
                
                <!-- Code & Rating -->
                <div class="flex items-center justify-between">
                  <span class="text-xl font-bold font-code text-white tracking-wide uppercase text-brand-orange drop-shadow-sm">
                    {{ item.code }}
                  </span>
                  <!-- Star Rating -->
                  <div class="flex items-center gap-0.5 text-xs">
                    <i v-for="star in 5" :key="star" 
                       :class="star <= item.rating ? 'fa-solid fa-star text-amber-400' : 'fa-solid fa-star text-slate-700'"></i>
                  </div>
                </div>

                <!-- Title -->
                <p class="text-xs text-slate-300 line-clamp-2 leading-relaxed">
                  {{ item.title || 'ไม่มีข้อมูลชื่อเรื่อง' }}
                </p>

                <!-- Actress Tagged -->
                <div v-if="item.actress" class="flex items-center gap-2 text-xs font-medium text-slate-300 bg-brand-dark p-2 rounded-xl border border-slate-800">
                  <div class="w-6 h-6 rounded-lg bg-brand-black flex items-center justify-center text-brand-orange text-[10px] border border-orange-500/20">
                    <i class="fa-solid fa-user-ninja"></i>
                  </div>
                  <span class="text-brand-orange font-bold">{{ item.actress }}</span>
                </div>

                <!-- Category Tags -->
                <div class="flex flex-wrap gap-1.5 pt-1">
                  <span v-for="tag in item.tags" :key="tag" 
                        @click="searchQuery = tag"
                        class="px-2.5 py-1 bg-brand-dark text-slate-400 text-[10px] font-medium rounded-lg border border-slate-800 cursor-pointer hover:text-brand-orange hover:border-brand-orange/40 transition">
                    #{{ tag }}
                  </span>
                </div>

                <!-- Card Action Controls -->
                <div class="flex items-center gap-2 pt-2 border-t border-slate-800/60">
                  <button @click="openEditModal(item)" class="flex-1 py-2 rounded-xl btn-dark-skeuo text-slate-300 text-xs font-medium flex items-center justify-center gap-1.5 border border-slate-800">
                    <i class="fa-solid fa-pen-to-square text-slate-400"></i> แก้ไข
                  </button>
                  <button @click="deleteItem(item)" class="flex-1 py-2 rounded-xl btn-dark-skeuo text-rose-400 text-xs font-medium flex items-center justify-center gap-1.5 border border-slate-800">
                    <i class="fa-solid fa-trash"></i> ลบ
                  </button>
                </div>

              </div>

            </div>
          </div>

        </div>

        <!-- TAB 2: ACTRESSES GALLERY (รูปดารา) -->
        <div v-if="activeTab === 'actresses'" class="space-y-4">
          
          <div class="flex items-center justify-between px-1">
            <h2 class="text-sm font-bold text-white flex items-center gap-2">
              <i class="fa-solid fa-heart text-brand-orange"></i> ดาราและนักแสดงยอดนิยม
            </h2>
            <span class="text-[11px] text-slate-500">{{ actressesList.length }} คน</span>
          </div>

          <!-- Actresses Grid -->
          <div class="grid grid-cols-2 gap-3">
            <div v-for="actress in actressesList" :key="actress.id" 
                 class="bg-brand-card shadow-skeuo-raised rounded-2xl p-3 border border-slate-800/80 flex flex-col items-center text-center relative overflow-hidden group">
              
              <!-- Actress Avatar Image Container with Blur -->
              <div class="relative w-24 h-24 rounded-full shadow-skeuo-inset overflow-hidden border-2 border-brand-orange/40 mb-2 bg-slate-900">
                <img :src="actress.photo" 
                     :class="(globalBlurMode || actress.isBlur) ? 'img-blur-hidden' : 'img-blur-visible'"
                     class="w-full h-full object-cover" :alt="actress.name">
                
                <!-- Click overlay to toggle blur -->
                <div @click="actress.isBlur = !actress.isBlur" class="absolute inset-0 cursor-pointer flex items-center justify-center bg-black/30 hover:bg-black/10">
                  <i v-if="globalBlurMode || actress.isBlur" class="fa-solid fa-eye-slash text-brand-orange text-sm drop-shadow-md"></i>
                </div>
              </div>

              <h3 class="text-xs font-bold text-white mb-0.5 line-clamp-1">{{ actress.name }}</h3>
              <p class="text-[10px] text-brand-orange font-code mb-2">{{ actress.jpName }}</p>

              <!-- Studio Tag -->
              <span class="px-2 py-0.5 rounded-md bg-brand-dark text-[9px] text-slate-400 border border-slate-800 mb-2">
                {{ actress.mainStudio }}
              </span>

              <!-- Filter by Actress Button -->
              <button @click="filterByActress(actress.name)" 
                      class="w-full py-1.5 rounded-xl btn-dark-skeuo text-brand-orange text-[11px] font-bold border border-slate-800 flex items-center justify-center gap-1">
                <i class="fa-solid fa-magnifying-glass text-[10px]"></i> ค้นหาผลงาน
              </button>

            </div>
          </div>

        </div>

        <!-- TAB 3: CATEGORIES & STUDIOS -->
        <div v-if="activeTab === 'categories'" class="space-y-6">
          
          <!-- Tags Section -->
          <div>
            <h2 class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-3 px-1">
              หมวดหมู่ยอดฮิต (Tags)
            </h2>
            <div class="grid grid-cols-2 gap-2.5">
              <button v-for="(count, tag) in allTagsWithCount" :key="tag"
                      @click="selectTagFilter(tag)"
                      class="bg-brand-card shadow-skeuo-raised p-3 rounded-xl border border-slate-800 flex items-center justify-between text-left active:scale-95 transition">
                <div class="flex items-center gap-2">
                  <i class="fa-solid fa-hashtag text-brand-orange text-xs"></i>
                  <span class="text-xs font-bold text-slate-200">{{ tag }}</span>
                </div>
                <span class="px-2 py-0.5 rounded-md bg-brand-dark text-[10px] font-code text-slate-400 border border-slate-800">
                  {{ count }}
                </span>
              </button>
            </div>
          </div>

          <!-- Studios Section -->
          <div>
            <h2 class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-3 px-1">
              ค่ายผู้ผลิต (Studios)
            </h2>
            <div class="grid grid-cols-2 gap-2.5">
              <button v-for="(count, studio) in allStudiosWithCount" :key="studio"
                      @click="selectStudioFilter(studio)"
                      class="bg-brand-card shadow-skeuo-raised p-3 rounded-xl border border-slate-800 flex items-center justify-between text-left active:scale-95 transition">
                <span class="text-xs font-bold font-code text-brand-orange uppercase">{{ studio }}</span>
                <span class="px-2 py-0.5 rounded-md bg-brand-dark text-[10px] font-code text-slate-400 border border-slate-800">
                  {{ count }} รายการ
                </span>
              </button>
            </div>
          </div>

        </div>

        <!-- TAB 4: ADD / EDIT CODE -->
        <div v-if="activeTab === 'add'" class="space-y-4">
          
          <div class="bg-brand-card shadow-skeuo-raised rounded-2xl p-4 border border-slate-800">
            
            <div class="flex items-center gap-3 mb-5 border-b border-slate-800/80 pb-3">
              <div class="w-10 h-10 rounded-xl bg-brand-dark shadow-skeuo-raised flex items-center justify-center text-brand-orange border border-orange-500/20">
                <i class="fa-solid fa-plus text-base"></i>
              </div>
              <div>
                <h2 class="text-base font-bold text-white">{{ form.id ? 'แก้ไขข้อมูลรหัส' : 'บันทึกรหัสใหม่' }}</h2>
                <p class="text-[11px] text-slate-400">กรอกรหัสวิดีโอเพื่อค้นหาและจัดหมวดหมู่</p>
              </div>
            </div>

            <form @submit.prevent="saveItem" class="space-y-4">
              
              <!-- Code Field -->
              <div>
                <label class="block text-xs font-bold text-slate-300 mb-1.5">รหัสหนัง (Code) *</label>
                <div class="relative">
                  <input type="text" v-model="form.code" @input="onCodeInput" placeholder="ตัวอย่าง: IPX-888, SSIS-001" required
                         class="w-full bg-brand-black shadow-skeuo-inset text-brand-orange font-code font-bold uppercase px-3.5 py-2.5 rounded-xl text-sm outline-none border border-slate-800 focus:border-brand-orange">
                  <span v-if="detectedStudio" class="absolute right-2.5 top-1/2 -translate-y-1/2 text-[10px] font-bold font-code px-2 py-0.5 rounded bg-brand-dark text-slate-300 border border-slate-700">
                    {{ detectedStudio }}
                  </span>
                </div>
              </div>

              <!-- Title -->
              <div>
                <label class="block text-xs font-bold text-slate-300 mb-1.5">ชื่อเรื่องย่อ / คำอธิบาย</label>
                <input type="text" v-model="form.title" placeholder="รายละเอียดเนื้อเรื่อง..."
                       class="w-full bg-brand-black shadow-skeuo-inset text-slate-200 px-3.5 py-2.5 rounded-xl text-xs outline-none border border-slate-800 focus:border-brand-orange">
              </div>

              <!-- Image URL (Custom photo link) -->
              <div>
                <label class="block text-xs font-bold text-slate-300 mb-1.5">ลิงก์รูปภาพปก (Optional)</label>
                <input type="url" v-model="form.imageUrl" placeholder="https://example.com/cover.jpg"
                       class="w-full bg-brand-black shadow-skeuo-inset text-slate-200 px-3.5 py-2.5 rounded-xl text-xs outline-none border border-slate-800 focus:border-brand-orange">
              </div>

              <!-- Actress -->
              <div>
                <label class="block text-xs font-bold text-slate-300 mb-1.5">ชื่อนักแสดง (Actress)</label>
                <input type="text" v-model="form.actress" placeholder="ชื่อนักแสดง..." list="actresses-list"
                       class="w-full bg-brand-black shadow-skeuo-inset text-slate-200 px-3.5 py-2.5 rounded-xl text-xs outline-none border border-slate-800 focus:border-brand-orange">
                <datalist id="actresses-list">
                  <option v-for="actress in actressesList" :key="actress.id" :value="actress.name"></option>
                </datalist>
              </div>

              <!-- Studio -->
              <div>
                <label class="block text-xs font-bold text-slate-300 mb-1.5">ค่ายผู้ผลิต (Studio)</label>
                <input type="text" v-model="form.studio" placeholder="เช่น IDEA POCKET, MOODYZ, S1"
                       class="w-full bg-brand-black shadow-skeuo-inset text-slate-200 uppercase px-3.5 py-2.5 rounded-xl text-xs outline-none border border-slate-800 focus:border-brand-orange">
              </div>

              <!-- Tags Selection -->
              <div>
                <label class="block text-xs font-bold text-slate-300 mb-1.5">เลือกหมวดหมู่ (Tags)</label>
                <div class="flex flex-wrap gap-1.5 mb-2.5 p-3 shadow-skeuo-inset rounded-xl bg-brand-black border border-slate-800/80">
                  <button type="button" v-for="tag in presetTags" :key="tag"
                          @click="toggleTagInForm(tag)"
                          :class="form.tags.includes(tag) ? 'btn-orange-skeuo font-bold' : 'btn-dark-skeuo text-slate-400'"
                          class="px-2.5 py-1 rounded-lg text-[11px] border border-slate-800 transition">
                    #{{ tag }}
                  </button>
                </div>
                <!-- Custom Tag Input -->
                <div class="flex gap-2">
                  <input type="text" v-model="customTagInput" placeholder="+ เพิ่มหมวดหมู่เอง" @keydown.enter.prevent="addCustomTag"
                         class="flex-1 bg-brand-black shadow-skeuo-inset text-slate-200 px-3 py-2 rounded-xl text-xs outline-none border border-slate-800">
                  <button type="button" @click="addCustomTag" class="px-4 btn-dark-skeuo text-brand-orange font-bold rounded-xl text-xs border border-slate-800">
                    เพิ่ม
                  </button>
                </div>
              </div>

              <!-- Rating & Watch Status -->
              <div class="grid grid-cols-2 gap-3">
                <div>
                  <label class="block text-xs font-bold text-slate-300 mb-1.5">สถานะการดู</label>
                  <select v-model="form.status" class="w-full bg-brand-black shadow-skeuo-inset text-slate-200 px-3 py-2.5 rounded-xl text-xs outline-none border border-slate-800">
                    <option value="PLAN">รอการรับชม</option>
                    <option value="WATCHED">รับชมแล้ว</option>
                  </select>
                </div>
                <div>
                  <label class="block text-xs font-bold text-slate-300 mb-1.5">คะแนนความชอบ</label>
                  <div class="flex items-center justify-around bg-brand-black shadow-skeuo-inset rounded-xl px-3 py-2 border border-slate-800">
                    <i v-for="star in 5" :key="star"
                       @click="form.rating = star"
                       :class="star <= form.rating ? 'fa-solid fa-star text-amber-400 scale-110' : 'fa-solid fa-star text-slate-700'"
                       class="text-xs cursor-pointer transition-transform"></i>
                  </div>
                </div>
              </div>

              <!-- Form Buttons -->
              <div class="flex gap-2 pt-2">
                <button type="button" v-if="form.id" @click="resetForm" class="flex-1 py-3 rounded-xl btn-dark-skeuo text-slate-400 font-bold text-xs border border-slate-800">
                  ยกเลิก
                </button>
                <button type="submit" class="flex-1 py-3 rounded-xl btn-orange-skeuo font-bold text-sm flex items-center justify-center gap-1.5">
                  <i class="fa-solid fa-floppy-disk"></i> {{ form.id ? 'อัปเดตข้อมูล' : 'บันทึกรหัส' }}
                </button>
              </div>

            </form>

          </div>

        </div>

        <!-- TAB 5: SETTINGS -->
        <div v-if="activeTab === 'settings'" class="space-y-4">
          
          <div class="bg-brand-card shadow-skeuo-raised rounded-2xl p-4 border border-slate-800 text-center">
            <div class="w-14 h-14 mx-auto rounded-2xl bg-brand-dark shadow-skeuo-raised flex items-center justify-center text-brand-orange border border-orange-500/20 mb-3">
              <i class="fa-solid fa-sliders text-xl"></i>
            </div>
            <h2 class="text-base font-bold text-white">ตั้งค่าระบบและความปลอดภัย</h2>
            <p class="text-[11px] text-slate-400 mt-0.5">จัดการรหัส PIN และสำรองข้อมูลส่วนตัว</p>
          </div>

          <!-- PWA Install Banner -->
          <div v-if="deferredPrompt" class="bg-brand-card shadow-skeuo-raised rounded-2xl p-3.5 border border-slate-800 flex items-center justify-between">
            <div class="flex items-center gap-3">
              <i class="fa-solid fa-download text-brand-orange text-lg"></i>
              <div>
                <h3 class="text-xs font-bold text-white">ติดตั้งแอปพลิเคชัน (PWA)</h3>
                <p class="text-[10px] text-slate-400">เพิ่มลงหน้าจอโฮมเพื่อใช้งานออฟไลน์</p>
              </div>
            </div>
            <button @click="installPWA" class="btn-orange-skeuo px-3.5 py-1.5 rounded-xl text-xs font-bold">
              ติดตั้ง
            </button>
          </div>

          <!-- Quick Actions -->
          <div class="bg-brand-card shadow-skeuo-raised rounded-2xl p-3.5 border border-slate-800 space-y-2.5">
            
            <button @click="promptChangePin" class="w-full flex items-center justify-between p-3 rounded-xl btn-dark-skeuo border border-slate-800 text-left">
              <div class="flex items-center gap-3">
                <i class="fa-solid fa-key text-brand-orange text-sm"></i>
                <span class="text-xs font-bold text-slate-200">เปลี่ยนรหัส PIN (ปัจจุบัน: {{ pinCode }})</span>
              </div>
              <i class="fa-solid fa-chevron-right text-xs text-slate-500"></i>
            </button>

            <button @click="exportData" class="w-full flex items-center justify-between p-3 rounded-xl btn-dark-skeuo border border-slate-800 text-left">
              <div class="flex items-center gap-3">
                <i class="fa-solid fa-file-export text-emerald-400 text-sm"></i>
                <span class="text-xs font-bold text-slate-200">สำรองข้อมูล (Export JSON)</span>
              </div>
              <i class="fa-solid fa-download text-xs text-slate-500"></i>
            </button>

            <label class="w-full flex items-center justify-between p-3 rounded-xl btn-dark-skeuo border border-slate-800 cursor-pointer text-left">
              <div class="flex items-center gap-3">
                <i class="fa-solid fa-file-import text-amber-400 text-sm"></i>
                <span class="text-xs font-bold text-slate-200">นำเข้าข้อมูล (Import JSON)</span>
              </div>
              <input type="file" accept=".json" @change="importData" class="hidden">
              <i class="fa-solid fa-upload text-xs text-slate-500"></i>
            </label>

          </div>

          <!-- Reset All Data -->
          <button @click="clearAllData" class="w-full py-3 bg-rose-950/40 hover:bg-rose-900/60 text-rose-400 font-bold text-xs rounded-xl border border-rose-800/50 flex items-center justify-center gap-2 transition">
            <i class="fa-solid fa-triangle-exclamation"></i> ล้างข้อมูลทั้งหมดในเครื่อง
          </button>

          <p class="text-center text-[10px] text-slate-600 font-code pt-2">CodeVault PWA v3.0 • Skeuomorphic Edition</p>
        </div>

      </main>

      <!-- BOTTOM NAVIGATION BAR -->
      <nav class="fixed bottom-3 left-1/2 -translate-x-1/2 w-[92%] max-w-sm bg-brand-dark/95 backdrop-blur-lg shadow-skeuo-raised rounded-2xl py-2 px-3 flex justify-around items-center z-40 border border-slate-800">
        
        <!-- Library Tab -->
        <button @click="activeTab = 'library'" 
                class="flex flex-col items-center justify-center gap-1 transition-all"
                :class="activeTab === 'library' ? 'text-brand-orange' : 'text-slate-500'">
          <i class="fa-solid fa-film text-base"></i>
          <span class="text-[9px] font-bold">คลังรหัส</span>
        </button>

        <!-- Actresses Tab -->
        <button @click="activeTab = 'actresses'" 
                class="flex flex-col items-center justify-center gap-1 transition-all"
                :class="activeTab === 'actresses' ? 'text-brand-orange' : 'text-slate-500'">
          <i class="fa-solid fa-users text-base"></i>
          <span class="text-[9px] font-bold">ดารา</span>
        </button>

        <!-- Center Add Button -->
        <button @click="activeTab = 'add'" 
                class="w-12 h-12 -mt-5 rounded-2xl btn-orange-skeuo flex items-center justify-center text-white border-2 border-brand-black shadow-orange-glow">
          <i class="fa-solid fa-plus text-xl transition-transform" :class="activeTab === 'add' ? 'rotate-45' : ''"></i>
        </button>

        <!-- Categories Tab -->
        <button @click="activeTab = 'categories'" 
                class="flex flex-col items-center justify-center gap-1 transition-all"
                :class="activeTab === 'categories' ? 'text-brand-orange' : 'text-slate-500'">
          <i class="fa-solid fa-icons text-base"></i>
          <span class="text-[9px] font-bold">หมวดหมู่</span>
        </button>

        <!-- Settings Tab -->
        <button @click="activeTab = 'settings'" 
                class="flex flex-col items-center justify-center gap-1 transition-all"
                :class="activeTab === 'settings' ? 'text-brand-orange' : 'text-slate-500'">
          <i class="fa-solid fa-gear text-base"></i>
          <span class="text-[9px] font-bold">ตั้งค่า</span>
        </button>

      </nav>

    </template>

  </div>

  <script>
    const { createApp, ref, computed, onMounted, watch } = Vue;

    createApp({
      setup() {
        // App Security & Lock State
        const isLocked = ref(true);
        const pinInput = ref('');
        const pinCode = ref(localStorage.getItem('codevault_pin') || '1234');
        const pinError = ref(false);

        // Global Blur Switch (Default TRUE for Privacy)
        const globalBlurMode = ref(true);

        // Navigation Tabs & Search
        const activeTab = ref('library');
        const searchQuery = ref('');
        const activeStatusFilter = ref('ALL');
        const sortBy = ref('newest');

        const deferredPrompt = ref(null);
        const items = ref([]);

        // Default Famous Actresses List with Avatar Images
        const actressesList = ref([
          { id: '1', name: 'Yua Mikami', jpName: '三上悠亜', mainStudio: 'IDEA POCKET', photo: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=300&auto=format&fit=crop&q=80', isBlur: true },
          { id: '2', name: 'Eimi Fukada', jpName: '深田えいみ', mainStudio: 'S1 NO.1 STYLE', photo: 'https://images.unsplash.com/photo-1517841905240-472988babdf9?w=300&auto=format&fit=crop&q=80', isBlur: true },
          { id: '3', name: 'Remu Suzumori', jpName: '涼森れむ', mainStudio: 'MOODYZ', photo: 'https://images.unsplash.com/photo-1524504388940-b1c1722653e1?w=300&auto=format&fit=crop&q=80', isBlur: true },
          { id: '4', name: 'Kana Momonogi', jpName: '桃乃木かな', mainStudio: 'IDEA POCKET', photo: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=300&auto=format&fit=crop&q=80', isBlur: true },
          { id: '5', name: 'Tsukasa Aoi', jpName: '葵つかさ', mainStudio: 'Alice Japan', photo: 'https://images.unsplash.com/photo-1529626455594-4ff0802cfb7e?w=300&auto=format&fit=crop&q=80', isBlur: true },
          { id: '6', name: 'Minami Aizawa', jpName: '相沢みなみ', mainStudio: 'FALENO star', photo: 'https://images.unsplash.com/photo-1508214751196-bcfd4ca60f91?w=300&auto=format&fit=crop&q=80', isBlur: true },
          { id: '7', name: 'Karen Kaede', jpName: '楓カレン', mainStudio: 'IDEA POCKET', photo: 'https://images.unsplash.com/photo-1544005313-94ddf0286df2?w=300&auto=format&fit=crop&q=80', isBlur: true }
        ]);

        // Preset Categories
        const presetTags = ref([
          'ชุดนักเรียน', 'พนักงานออฟฟิศ', 'คอสเพลย์', 'ซับไทย', 
          'ความคมชัดสูง HD', 'ยอดนิยม', 'โรแมนติก', 'พยาบาล'
        ]);

        const studioMap = {
          'IPX': 'IDEA POCKET', 'SSIS': 'S1 NO.1 STYLE', 'MIDV': 'MOODYZ',
          'CAWD': 'KAWaii', 'STARS': 'SOD', 'SONE': 'S1 NO.1 STYLE',
          'FALENO': 'FALENO star', 'MIDE': 'MOODYZ', 'PRED': 'PREMIUM', 'ATID': 'ATTACKERS'
        };

        const form = ref({ 
          id: null, code: '', title: '', imageUrl: '', actress: '', 
          studio: '', tags: [], status: 'PLAN', rating: 3, isFavorite: false, isBlur: true 
        });
        
        const customTagInput = ref('');
        const detectedStudio = ref('');

        // Fallback photo generator for code cards
        const getFallbackImage = (code) => {
          const cleanCode = (code || 'AV').replace(/[^a-zA-Z0-9]/g, '');
          return `https://picsum.photos/seed/${cleanCode}/400/280`;
        };

        const handleImgError = (event, code) => {
          event.target.src = getFallbackImage(code);
        };

        // Load Initial Saved Data
        const loadInitialData = () => {
          const saved = localStorage.getItem('codevault_data');
          if (saved) {
            try { 
              items.value = JSON.parse(saved); 
              return; 
            } catch(e) {}
          }
          // Demo Data
          items.value = [
            { id: '1', code: 'IPX-888', title: 'ผลงานระดับพรีเมียม ซับไทยคุณภาพสูง', imageUrl: '', actress: 'Yua Mikami', studio: 'IDEA POCKET', tags: ['ยอดนิยม', 'ซับไทย', 'ความคมชัดสูง HD'], status: 'WATCHED', rating: 5, isFavorite: true, isBlur: true, createdAt: Date.now() - 1000 },
            { id: '2', code: 'SSIS-001', title: 'บทบาทพนักงานออฟฟิศสาวสุดน่ารัก', imageUrl: '', actress: 'Eimi Fukada', studio: 'S1 NO.1 STYLE', tags: ['พนักงานออฟฟิศ', 'คอสเพลย์'], status: 'PLAN', rating: 4, isFavorite: false, isBlur: true, createdAt: Date.now() - 2000 },
            { id: '3', code: 'MIDV-123', title: 'การแสดงสุดประทับใจ', imageUrl: '', actress: 'Remu Suzumori', studio: 'MOODYZ', tags: ['คอสเพลย์', 'ชุดนักเรียน'], status: 'WATCHED', rating: 5, isFavorite: true, isBlur: true, createdAt: Date.now() - 3000 }
          ];
          saveToLocalStorage();
        };

        const saveToLocalStorage = () => { 
          localStorage.setItem('codevault_data', JSON.stringify(items.value)); 
        };
        watch(items, saveToLocalStorage, { deep: true });

        // PIN Keypad Handlers
        const appendPin = (num) => {
          if (pinInput.value.length < 4) {
            pinInput.value += num;
            pinError.value = false;
            if (pinInput.value.length === 4) verifyPin();
          }
        };
        const deletePin = () => { pinInput.value = pinInput.value.slice(0, -1); };
        const clearPin = () => { pinInput.value = ''; };
        
        const verifyPin = () => {
          if (pinInput.value === pinCode.value) { 
            isLocked.value = false; 
            pinInput.value = ''; 
          } else { 
            pinError.value = true; 
            setTimeout(() => { pinInput.value = ''; }, 400); 
          }
        };
        
        const lockApp = () => { 
          isLocked.value = true; 
          pinInput.value = ''; 
        };
        
        const promptChangePin = () => {
          const newPin = prompt('กรอกรหัส PIN ใหม่ 4 หลัก:', pinCode.value);
          if (newPin && newPin.length === 4 && !isNaN(newPin)) {
            pinCode.value = newPin;
            localStorage.setItem('codevault_pin', newPin);
            alert('เปลี่ยนรหัส PIN สำเร็จ!');
          } else if (newPin) {
            alert('โปรดกรอกตัวเลข 4 หลักเท่านั้น');
          }
        };

        // Blur Image Individual Toggle
        const toggleItemBlur = (item) => {
          item.isBlur = !item.isBlur;
        };

        // Code Prefix Studio Auto Detection
        const onCodeInput = () => {
          const raw = form.value.code.toUpperCase().trim();
          form.value.code = raw;
          const match = raw.match(/^([A-Z0-9]+)/);
          if (match && match[1]) {
            const prefix = match[1];
            form.value.studio = studioMap[prefix] || prefix;
            detectedStudio.value = studioMap[prefix] || prefix;
          } else { 
            detectedStudio.value = ''; 
          }
        };

        const toggleTagInForm = (tag) => {
          const idx = form.value.tags.indexOf(tag);
          if (idx >= 0) form.value.tags.splice(idx, 1);
          else form.value.tags.push(tag);
        };

        const addCustomTag = () => {
          const val = customTagInput.value.trim();
          if (val && !form.value.tags.includes(val)) {
            form.value.tags.push(val);
            if (!presetTags.value.includes(val)) presetTags.value.push(val);
            customTagInput.value = '';
          }
        };

        const saveItem = () => {
          if (!form.value.code) return;
          if (form.value.id) {
            const idx = items.value.findIndex(i => i.id === form.value.id);
            if (idx >= 0) items.value[idx] = { ...form.value };
          } else {
            items.value.unshift({ 
              ...form.value, 
              id: Date.now().toString(), 
              createdAt: Date.now(),
              isBlur: true 
            });
          }
          resetForm();
          activeTab.value = 'library';
        };

        const resetForm = () => {
          form.value = { 
            id: null, code: '', title: '', imageUrl: '', actress: '', 
            studio: '', tags: [], status: 'PLAN', rating: 3, isFavorite: false, isBlur: true 
          };
          detectedStudio.value = '';
        };

        const openEditModal = (item) => { 
          form.value = JSON.parse(JSON.stringify(item)); 
          activeTab.value = 'add'; 
        };

        const deleteItem = (item) => { 
          if (confirm(`ต้องการลบรหัส ${item.code} หรือไม่?`)) {
            items.value = items.value.filter(i => i.id !== item.id);
          }
        };

        const toggleFavorite = (item) => { 
          item.isFavorite = !item.isFavorite; 
        };

        const filterByActress = (name) => {
          searchQuery.value = name;
          activeTab.value = 'library';
        };

        // Computed Filtered Items
        const filteredItems = computed(() => {
          let list = [...items.value];
          
          if (activeStatusFilter.value === 'FAVORITE') {
            list = list.filter(i => i.isFavorite);
          } else if (activeStatusFilter.value === 'WATCHED') {
            list = list.filter(i => i.status === 'WATCHED');
          } else if (activeStatusFilter.value === 'PLAN') {
            list = list.filter(i => i.status === 'PLAN');
          }
          
          if (searchQuery.value.trim()) {
            const q = searchQuery.value.toLowerCase().trim();
            list = list.filter(i => 
              (i.code || '').toLowerCase().includes(q) || 
              (i.title || '').toLowerCase().includes(q) || 
              (i.actress || '').toLowerCase().includes(q) || 
              (i.studio || '').toLowerCase().includes(q) ||
              (i.tags || []).some(t => t.toLowerCase().includes(q))
            );
          }

          if (sortBy.value === 'newest') list.sort((a, b) => b.createdAt - a.createdAt);
          else if (sortBy.value === 'code') list.sort((a, b) => a.code.localeCompare(b.code));
          else if (sortBy.value === 'rating') list.sort((a, b) => b.rating - a.rating);
          
          return list;
        });

        // Tags and Studio Counts
        const allTagsWithCount = computed(() => {
          const counts = {};
          items.value.forEach(i => (i.tags || []).forEach(t => counts[t] = (counts[t] || 0) + 1));
          return counts;
        });

        const allStudiosWithCount = computed(() => {
          const counts = {};
          items.value.forEach(i => { const s = i.studio || 'GENERAL'; counts[s] = (counts[s] || 0) + 1; });
          return counts;
        });

        const selectTagFilter = (tag) => { searchQuery.value = tag; activeTab.value = 'library'; };
        const selectStudioFilter = (studio) => { searchQuery.value = studio; activeTab.value = 'library'; };

        // Export/Import JSON Data Backup
        const exportData = () => {
          const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(items.value));
          const dl = document.createElement('a'); 
          dl.setAttribute("href", dataStr); 
          dl.setAttribute("download", `codevault_backup_${new Date().toISOString().slice(0,10)}.json`); 
          dl.click();
        };

        const importData = (event) => {
          const file = event.target.files[0]; 
          if (!file) return;
          const reader = new FileReader();
          reader.onload = (e) => {
            try { 
              const imported = JSON.parse(e.target.result); 
              if (Array.isArray(imported)) {
                items.value = imported; 
                alert('นำเข้าข้อมูลสำเร็จแล้ว!'); 
              }
            } catch(err) { 
              alert('ไฟล์ JSON ไม่ถูกต้อง'); 
            }
          };
          reader.readAsText(file);
        };

        const clearAllData = () => {
          if (confirm('ยืนยันล้างข้อมูลรหัสทั้งหมดในคลัง?')) { 
            items.value = []; 
            localStorage.removeItem('codevault_data'); 
          }
        };

        // PWA Installation Handler
        const setupPWA = () => { 
          window.addEventListener('beforeinstallprompt', (e) => { 
            e.preventDefault(); 
            deferredPrompt.value = e; 
          }); 
        };

        const installPWA = () => {
          if (deferredPrompt.value) { 
            deferredPrompt.value.prompt(); 
            deferredPrompt.value.userChoice.then(() => { deferredPrompt.value = null; }); 
          }
        };

        onMounted(() => { 
          loadInitialData(); 
          setupPWA(); 
        });

        return {
          isLocked, pinInput, pinCode, pinError, appendPin, deletePin, clearPin, lockApp, promptChangePin,
          globalBlurMode, toggleItemBlur, activeTab, searchQuery, activeStatusFilter, sortBy, 
          items, filteredItems, actressesList, presetTags, form, customTagInput, detectedStudio,
          getFallbackImage, handleImgError, onCodeInput, toggleTagInForm, addCustomTag, 
          saveItem, resetForm, openEditModal, deleteItem, toggleFavorite, filterByActress,
          allTagsWithCount, allStudiosWithCount, selectTagFilter, selectStudioFilter,
          exportData, importData, clearAllData, deferredPrompt, installPWA
        };
      }
    }).mount('#app');
  </script>
</body>
</html>
