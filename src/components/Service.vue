<!-- components/Service.vue -->
<template>
  <section 
    id="service" 
    class="min-h-screen bg-white flex items-center justify-center py-20"
  >
    <div class="container mx-auto px-4">
      <div 
        class="text-center transition-all duration-1000"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'"
      >
        <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-6">
          서비스
        </h2>
        <p class="text-lg text-gray-600 mb-12">
          STUDYforME의 다양한 서비스를 소개합니다
        </p>
        
        <!-- 서비스 내용 추가 -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mt-12">
          <div class="p-6 bg-purple-50 rounded-lg">
            <h3 class="text-xl font-bold mb-4">맞춤 추천</h3>
            <p class="text-gray-600">AI 기반 문제집 추천</p>
          </div>
          <div class="p-6 bg-purple-50 rounded-lg">
            <h3 class="text-xl font-bold mb-4">학습 분석</h3>
            <p class="text-gray-600">상세한 학습 리포트</p>
          </div>
          <div class="p-6 bg-purple-50 rounded-lg">
            <h3 class="text-xl font-bold mb-4">목표 관리</h3>
            <p class="text-gray-600">체계적인 학습 계획</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const isVisible = ref(false);

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true;
        }
      });
    },
    { threshold: 0.2 }
  );

  const section = document.getElementById('service');
  if (section) {
    observer.observe(section);
  }
});
</script>
