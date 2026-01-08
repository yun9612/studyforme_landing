<!-- components/Review.vue -->
<template>
  <section 
    id="review" 
    class="min-h-screen bg-gray-50 flex items-center justify-center py-20"
  >
    <div class="container mx-auto px-4">
      <div 
        class="text-center transition-all duration-1000"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'"
      >
        <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-6">
          리뷰
        </h2>
        <p class="text-lg text-gray-600 mb-12">
          사용자들의 생생한 후기를 확인하세요
        </p>
        
        <!-- 리뷰 내용 추가 -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 mt-12">
          <div class="p-6 bg-white rounded-lg shadow-md">
            <div class="flex items-center mb-4">
              <div class="w-12 h-12 bg-purple-500 rounded-full flex items-center justify-center text-white font-bold">
                A
              </div>
              <div class="ml-4 text-left">
                <p class="font-bold">학생 A</p>
                <p class="text-sm text-gray-500">고3</p>
              </div>
            </div>
            <p class="text-gray-600 text-left">
              "문제집 추천이 정말 정확해요. 성적이 많이 올랐습니다!"
            </p>
          </div>
          
          <div class="p-6 bg-white rounded-lg shadow-md">
            <div class="flex items-center mb-4">
              <div class="w-12 h-12 bg-purple-500 rounded-full flex items-center justify-center text-white font-bold">
                B
              </div>
              <div class="ml-4 text-left">
                <p class="font-bold">학생 B</p>
                <p class="text-sm text-gray-500">고2</p>
              </div>
            </div>
            <p class="text-gray-600 text-left">
              "학습 분석 기능이 너무 유용해요. 약점을 파악하기 좋아요."
            </p>
          </div>
          
          <div class="p-6 bg-white rounded-lg shadow-md">
            <div class="flex items-center mb-4">
              <div class="w-12 h-12 bg-purple-500 rounded-full flex items-center justify-center text-white font-bold">
                C
              </div>
              <div class="ml-4 text-left">
                <p class="font-bold">학생 C</p>
                <p class="text-sm text-gray-500">고1</p>
              </div>
            </div>
            <p class="text-gray-600 text-left">
              "목표 관리 기능 덕분에 계획적으로 공부할 수 있어요."
            </p>
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

  const section = document.getElementById('review');
  if (section) {
    observer.observe(section);
  }
});
</script>
