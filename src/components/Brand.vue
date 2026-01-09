<!-- components/Brand.vue -->
<template>
  <section
    id="brand"
    class="relative overflow-hidden bg-linear-to-br from-[#652BDF] to-[#8e5aff] md:from-[#8e5aff] md:to-[#652BDF]">
    <!-- 배경 장식 요소
    <div class="absolute top-1/4 left-10 w-32 h-32 bg-purple-400 rounded-full opacity-20 blur-3xl"></div>
    <div class="absolute bottom-1/4 right-10 w-40 h-40 bg-purple-300 rounded-full opacity-20 blur-3xl"></div> -->

    <!-- 메인 컨텐츠 -->
    <div class="container mx-auto px-4 flex items-center justify-center pt-15 md:pt-40">
      <div class="flex flex-col items-center text-center w-full max-w-6xl">
        <!-- 텍스트 영역 -->
        <!-- md일 때만 표시되는 p 태그 -->
        <p class="block md:hidden text-[#cbb2ff] font-bold text-sm mb-3">2024년 12월 출시</p>
        <div
          class="flex flex-col items-center mb-8 md:mb-12 transition-all duration-1000 delay-200"
          :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
          <p class="text-white text-3xl md:text-[34px] leading-10 font-bold mb-3 md:mb-7">
            최상위권을 향한<br class="md:hidden" />
            문제집 추천 앱
          </p>

          <img class="h-8 md:h-14 mb-12" src="/images/logo.png" alt="logo" />

          <!-- 다운로드 버튼 -->
          <button
            class="inline-flex items-center gap-2 px-6 py-3 bg-transparent border border-white text-white rounded-full hover:bg-white hover:text-purple-600 transition-all duration-300 text-[15px] md:text-base font-medium"
            @click="handleDownload">
            <svg class="w-4 h-4 md:w-5 md:h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            <span class="hidden md:inline">스터디포미 다운받기</span>
            <span class="inline md:hidden">앱 다운로드</span>
          </button>
        </div>

        <!-- 스마트폰 이미지 -->
        <div
          class="w-full flex justify-center transition-all duration-1000 delay-500"
          :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-16'">
          <div class="relative w-full">
            <img src="/images/phone-mockup.png" alt="STUDYforME 앱 화면" class="w-full h-auto drop-shadow-2xl" />
            <div class="absolute inset-0 bg-purple-400 opacity-20 blur-3xl -z-10 scale-90"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const isLoaded = ref(false);
let observer = null;

const handleDownload = () => {
  window.open("https://your-app-store-link", "_blank");
};

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        isLoaded.value = entry.isIntersecting;
      });
    },
    { threshold: 0.2 }
  );

  const section = document.getElementById("brand");
  if (section) {
    observer.observe(section);
  }
});

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>
