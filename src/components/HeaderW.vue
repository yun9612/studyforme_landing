<!-- components/Header.vue -->
<template>
  <header 
    class="fixed top-0 w-full transition-all duration-500 hidden md:block"
    :class="[
      isScrolled ? 'bg-[#8453ee] shadow-lg py-4 z-50' : 'bg-transparent py-4 z-50',
    ]"
  >
    <div 
      class="container mx-auto flex items-center transition-all duration-1000"
      :class="[
        isScrolled ? 'justify-between' : 'justify-end',
        isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 -translate-y-4'
      ]"
    >
      <!-- 로고 (스크롤 시 표시) -->
      <transition name="fade">
        <div 
          v-if="isScrolled"
          class="flex items-center"
        >
          <img 
            src="/images/logo.png" 
            alt="STUDYforME Logo" 
            class="h-5"
          />
        </div>
      </transition>

      <!-- 네비게이션 메뉴 -->
      <nav
        class="flex gap-6 md:gap-8 transition-all duration-500"
        :class="isScrolled ? 'text-lg' : 'text-sm md:text-base'"
      >
        <a
          v-for="menu in menus"
          :key="menu.id"
          :href="`#${menu.id}`"
          @click.prevent="scrollToSection(menu.id)"
          class="text-white transition-all duration-300 cursor-pointer hover:opacity-80"
          :class="activeSection === menu.id ? 'font-bold' : 'font-medium'"
        >
          {{ menu.name }}
        </a>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isLoaded = ref(false);
const isScrolled = ref(false);
const activeSection = ref('brand');

const menus = [
  { id: 'brand', name: '브랜드' },
  { id: 'service', name: '서비스' },
  { id: 'review', name: '리뷰' },
  { id: 'download', name: '다운로드' }
];

// 스크롤 이벤트 핸들러
const handleScroll = () => {
  isScrolled.value = window.scrollY > 100;
  
  // 현재 활성 섹션 감지
  const sections = menus.map(menu => ({
    id: menu.id,
    element: document.getElementById(menu.id)
  }));

  for (const section of sections) {
    if (section.element) {
      const rect = section.element.getBoundingClientRect();
      if (rect.top <= 100 && rect.bottom >= 100) {
        activeSection.value = section.id;
        break;
      }
    }
  }
};

// 섹션으로 스크롤
const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId);
  if (element) {
    const elementPosition = element.offsetTop;
    
    window.scrollTo({
      top: elementPosition,
      behavior: 'smooth'
    });
  }
};

onMounted(() => {
  isLoaded.value = true;
  
  window.addEventListener('scroll', handleScroll);
  handleScroll();
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
