<!-- components/Video.vue -->
<template>
  <section id="video" class="min-h-screen bg-white md:flex items-center justify-center py-20 hidden">
    <div class="container mx-auto px-4">
      <!-- 헤더 -->
      <div
        class="text-center transition-all duration-1000"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <p class="text-purple-600 text-sm md:text-base font-bold mb-6">Video</p>
        <h2 class="text-3xl md:text-[54px] font-bold text-gray-900">
          <span class="block lg:inline">스터디포미,</span>
          <span class="block lg:inline"> 더 자세히 알아볼까요?</span>
        </h2>
      </div>

      <!-- 비디오 영역 -->
      <div
        class="mt-12 md:mt-16 max-w-4xl mx-auto transition-all duration-1000 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <div class="relative rounded-2xl overflow-hidden shadow-2xl bg-gray-900 aspect-video">
          <!-- YouTube 비디오 임베드 -->
          <iframe
            class="w-full h-full"
            src="https://www.youtube.com/embed/RxpP82ipC9M"
            title="스터디포미 소개 영상"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
            referrerpolicy="strict-origin-when-cross-origin"></iframe>
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

  const section = document.getElementById("video");
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
