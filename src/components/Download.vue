<!-- components/Download.vue -->
<template>
  <section id="download" class="bg-[#652bdf] flex items-center justify-center py-30">
    <div class="container mx-auto px-4">
      <div
        class="text-center transition-all duration-1000"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <!-- 상단 라벨 -->
        <p class="text-[#c6aef7] text-sm md:text-base font-bold mb-6">앱 다운로드</p>

        <!-- 메인 헤딩 -->
        <h2 class="text-white text-md lg:text-[40px] font-bold mb-2 leading-tight">
          최상위권을 향한 문제집 추천 서비스
        </h2>
        <h2 class="text-white text-3xl md:text-[40px] font-bold mb-8 leading-tight">
          스터디포미를<br class="block md:hidden" />
          지금 만나보세요
        </h2>

        <!-- 설명 텍스트 -->
        <p class="text-purple-100 text-base mb-13 max-w-2xl mx-auto md:mb-22">
          아래 버튼을 클릭하시면<br class="block md:hidden" />
          해당 사이트로 이동합니다.
        </p>

        <!-- 다운로드 버튼 -->
        <div
          class="flex flex-col sm:flex-row gap-4 justify-center items-center transition-all duration-1000 delay-200"
          :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
          <!-- Google Play 버튼 -->
          <button
            @click="downloadApp('android')"
            class="bg-white w-30 h-10 p-3 rounded-sm md:w-40 md:h-15 md:rounded-lg transition-transform duration-300">
            <img src="/images/googleplay.png" alt="Google Play에서 다운로드" class="w-full" />
          </button>

          <!-- App Store 버튼 -->
          <button
            @click="downloadApp('ios')"
            class="bg-white h-10 w-30 p-2 rounded-sm md:w-40 md:h-15 md:p-3 md:rounded-lg transition-transform duration-300">
            <img src="/images/appstore.png" alt="App Store에서 다운로드" class="h-full" />
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const isVisible = ref(false);
let observer = null;

const downloadApp = (platform) => {
  if (platform === "android") {
    window.open("https://play.google.com/store/apps/details?id=com.studyforme.app", "_blank");
  } else if (platform === "ios") {
    window.open("https://apps.apple.com/kr/app/studyforme/id6496861038", "_blank");
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

  const section = document.getElementById("download");
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
