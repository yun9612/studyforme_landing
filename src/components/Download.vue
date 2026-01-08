<!-- components/Download.vue -->
<template>
  <section id="download" class="min-h-screen bg-linear-to-br from-[#BDA1FA] to-[#652BDF] flex items-center justify-center py-20">
    <div class="container mx-auto px-4">
      <div
        class="text-center transition-all duration-1000"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <h2 class="text-4xl md:text-5xl font-bold text-white mb-6">지금 바로 시작하세요</h2>
        <p class="text-lg text-purple-100 mb-12">STUDYforME와 함께 최상위권으로 도약하세요</p>

        <!-- 다운로드 버튼들 -->
        <div class="flex flex-col sm:flex-row gap-4 justify-center items-center mb-16">
          <button
            @click="downloadApp('ios')"
            class="flex items-center gap-3 px-8 py-4 bg-white text-purple-600 rounded-full hover:bg-purple-50 transition-all duration-300 font-bold text-lg shadow-lg hover:shadow-xl transform hover:-translate-y-1">
            <svg class="w-8 h-8" viewBox="0 0 24 24" fill="currentColor">
              <path
                d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z" />
            </svg>
            <div class="text-left">
              <p class="text-xs text-purple-400">Download on the</p>
              <p class="text-lg font-bold">App Store</p>
            </div>
          </button>

          <button
            @click="downloadApp('android')"
            class="flex items-center gap-3 px-8 py-4 bg-white text-purple-600 rounded-full hover:bg-purple-50 transition-all duration-300 font-bold text-lg shadow-lg hover:shadow-xl transform hover:-translate-y-1">
            <svg class="w-8 h-8" viewBox="0 0 24 24" fill="currentColor">
              <path
                d="M3,20.5V3.5C3,2.91 3.34,2.39 3.84,2.15L13.69,12L3.84,21.85C3.34,21.6 3,21.09 3,20.5M16.81,15.12L6.05,21.34L14.54,12.85L16.81,15.12M20.16,10.81C20.5,11.08 20.75,11.5 20.75,12C20.75,12.5 20.53,12.9 20.18,13.18L17.89,14.5L15.39,12L17.89,9.5L20.16,10.81M6.05,2.66L16.81,8.88L14.54,11.15L6.05,2.66Z" />
            </svg>
            <div class="text-left">
              <p class="text-xs text-purple-400">GET IT ON</p>
              <p class="text-lg font-bold">Google Play</p>
            </div>
          </button>
        </div>

        <!-- QR 코드 영역 (선택사항) -->
        <div class="flex flex-col items-center">
          <p class="text-purple-100 mb-4">QR 코드로 빠르게 다운로드</p>
          <div class="bg-white p-6 rounded-2xl shadow-xl">
            <div class="w-48 h-48 bg-gray-200 flex items-center justify-center">
              <!-- QR 코드 이미지 또는 생성 라이브러리 사용 -->
              <img src="" alt="QR Code" class="w-full h-full" />
            </div>
          </div>
        </div>

        <!-- 추가 정보 -->
        <div class="mt-16 grid grid-cols-1 md:grid-cols-3 gap-8 text-white">
          <div>
            <div class="text-3xl font-bold mb-2">10만+</div>
            <p class="text-purple-200">다운로드</p>
          </div>
          <div>
            <div class="text-3xl font-bold mb-2">4.8★</div>
            <p class="text-purple-200">평균 평점</p>
          </div>
          <div>
            <div class="text-3xl font-bold mb-2">98%</div>
            <p class="text-purple-200">만족도</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isVisible = ref(false);
let observer = null;

const downloadApp = (platform) => {
  if (platform === 'ios') {
    window.open('https://apps.apple.com/your-app-link', '_blank');
  } else if (platform === 'android') {
    window.open('https://play.google.com/store/apps/your-app-link', '_blank');
  }
};

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        isVisible.value = entry.isIntersecting;
      });
    },
    { threshold: 0.2 }
  );

  const section = document.getElementById('download');
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
