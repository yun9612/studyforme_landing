<!-- components/Service.vue -->
<template>
  <section id="service" class="min-h-screen bg-white flex items-center justify-center py-12 md:py-20">
    <div class="container mx-auto max-w-6xl px-4">
      <!-- 헤더 -->
      <div
        class="text-center mb-10 md:mb-16 transition-all duration-1000"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <p class="text-[#652BDF] text-sm md:text-base font-bold mb-4">Main Service</p>
        <h2 class="text-3xl md:text-[54px] font-bold text-gray-900 mb-2">문제집 선택,</h2>
        <h2 class="text-3xl md:text-[54px] font-bold text-gray-900">이제 고민하지 마세요</h2>
      </div>

      <!-- 서비스 카드 1 -->
      <div
        class="flex flex-col md:flex-row items-center gap-8 md:gap-16 mb-20 transition-all duration-1000 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <!-- 이미지 -->
        <div class="w-2/3 md:w-full flex justify-center md:justify-start">
          <div class="relative w-full max-w-md overflow-hidden rounded-4xl">
            <img src="/images/box__등록.png" alt="학습경험 입력" class="w-full h-auto" />
          </div>
        </div>

        <!-- 텍스트 -->
        <div class="w-5/6 md:w-full text-left">
          <p class="text-[#652BDF] text-sm md:text-[22px] font-bold mb-2 md:mb-4">학습 히스토리 관리</p>
          <h3 class="text-2xl md:text-[44px] font-bold text-gray-900 mb-3 md:mb-8">빠른 학습경험 입력</h3>
          <p class="text-gray-600 text-base md:text-xl">
            17초만에 학습 경험을 입력하면,<br />
            학습 히스토리가 차곡차곡 누적돼요.
          </p>
        </div>
      </div>

      <!-- 서비스 카드 2 -->
      <div
        class="flex flex-col md:flex-row-reverse items-center gap-8 md:gap-16 mb-20 transition-all duration-1000 delay-400"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <!-- 이미지 -->
        <div class="w-2/3 md:w-full flex justify-center md:justify-end">
          <div class="relative w-full max-w-md overflow-hidden rounded-4xl">
            <img src="/images/box_데이터.png" alt="학습경험" class="w-full h-auto" />
          </div>
        </div>

        <!-- 텍스트 -->
        <div class="w-5/6 md:w-full text-left">
          <p class="text-[#652BDF] text-sm md:text-[22px] font-bold mb-2 md:mb-4">학습결과 데이터 분석</p>
          <h3 class="text-2xl md:text-[44px] font-bold text-gray-900 mb-3 md:mb-8">
            AI가 분석해주는<br />
            학습경험
          </h3>
          <p class="text-gray-600 text-base md:text-xl">학습경험을 쌓을때마 분석해드려요.</p>
        </div>
      </div>

      <!-- 서비스 카드 3 -->
      <div
        class="flex flex-col md:flex-row items-center gap-8 md:gap-16 mb-20 transition-all duration-1000 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <!-- 이미지 -->
        <div class="w-2/3 md:w-full flex justify-center md:justify-start">
          <div class="relative w-full max-w-md overflow-hidden rounded-4xl">
            <img src="/images/box_추천.png" alt="문제집 추천" class="w-full h-auto" />
          </div>
        </div>

        <!-- 텍스트 -->
        <div class="w-5/6 md:w-full text-left">
          <p class="text-[#652BDF] text-sm md:text-[22px] font-bold mb-2 md:mb-4">문제집 추천</p>
          <h3 class="text-2xl md:text-[44px] font-bold text-gray-900 mb-3 md:mb-8">AI가 추천해주는<br />문제집 확인</h3>
          <p class="text-gray-600 text-base md:text-xl">
            입력한 학습경험 정보를 기반으로<br />
            다음 단곙 딱 맞는 문제집을 추천해드려요.
          </p>
        </div>
      </div>

      <!-- 서비스 카드 4 -->
      <div
        class="flex flex-col md:flex-row-reverse items-center gap-8 md:gap-16 transition-all duration-1000 delay-400"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <!-- 이미지 -->
        <div class="w-2/3 md:w-full flex justify-center md:justify-end">
          <div class="relative w-full max-w-md overflow-hidden rounded-4xl">
            <img src="/images/box_쇼핑.png" alt="문제집 구입" class="w-full h-auto" />
          </div>
        </div>

        <!-- 텍스트 -->
        <div class="w-5/6 md:w-full text-left">
          <p class="text-[#652BDF] text-sm md:text-[22px] font-bold mb-2 md:mb-4">문제집 구입</p>
          <h3 class="text-2xl md:text-[44px] font-bold text-gray-900 mb-3 md:mb-8">
            추천받은 문제집을<br />
            바로 구매
          </h3>
          <p class="text-gray-600 text-base md:text-xl">추천받은 문제집을 앱 내에서<br />편리하게 구매할 수 있어요.</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const isVisible = ref(false);
let observer = null;

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        isVisible.value = entry.isIntersecting;
      });
    },
    { threshold: 0.2 }
  );

  const section = document.getElementById("service");
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
