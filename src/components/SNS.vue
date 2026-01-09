<!-- components/SNS.vue -->
<template>
  <section id="sns" class="py-16 md:py-20 bg-[#161518]">
    <div class="container mx-auto px-4">
      <div
        class="text-center transition-all duration-1000"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <!-- 상단 라벨 -->
        <p class="text-[#713ce4] text-sm md:text-base font-bold mb-2">SNS</p>

        <!-- 헤딩 -->
        <h2 class="text-white text-xl md:text-[26px] font-bold mb-8">스터디포미 더 알아보기</h2>

        <!-- SNS 아이콘 -->
        <div
          class="flex gap-4 justify-center items-center transition-all duration-1000 delay-200"
          :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
          <!-- Instagram -->
          <a
            href="https://www.instagram.com/studyforme_official/"
            target="_blank"
            rel="noopener noreferrer"
            class="w-14 h-14 md:w-16 md:h-16 bg-white rounded-full flex items-center justify-center transition-transform duration-300 shadow-lg">
            <img src="/images/insta.png" alt="Instagram" class="w-7 h-7" />
          </a>

          <!-- Naver Blog -->
          <a
            href="https://blog.naver.com/studyforme_"
            target="_blank"
            rel="noopener noreferrer"
            class="w-14 h-14 md:w-16 md:h-16 bg-white rounded-full flex items-center justify-center transition-transform duration-300 shadow-lg">
            <img src="/images/blog.png" alt="Naver Blog" class="w-7 h-7" />
          </a>

          <!-- Kakao -->
          <div
            class="cursor-pointer w-14 h-14 md:w-16 md:h-16 bg-white rounded-full flex items-center justify-center transition-transform duration-300 shadow-lg">
            <img src="/images/kakao.png" alt="Naver Blog" class="w-7 h-7" />
          </div>
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

  const section = document.getElementById("sns");
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
