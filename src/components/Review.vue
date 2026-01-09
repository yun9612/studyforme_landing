<!-- components/Review.vue -->
<template>
  <section
    id="review"
    class="min-h-screen flex items-center justify-center py-12 md:py-20"
    style="background-color: #f2ecfe">
    <div class="container mx-auto max-w-6xl px-4">
      <!-- 헤더 -->
      <div
        class="mb-10 md:mb-16 transition-all duration-1000 text-center md:text-left"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <p class="text-[#652BDF] text-sm md:text-base font-bold mb-4">User Review</p>
        <h2 class="text-3xl md:text-[54px] font-bold text-gray-900 mb-2">스터디포미 사용 후</h2>
        <h2 class="text-3xl md:text-[54px] font-bold text-gray-900">어떤 점이 달라졌나요?</h2>
      </div>

      <!-- 모바일: 2열 그리드 (768px 미만) -->
      <div
        class="grid grid-cols-2 gap-2 md:hidden transition-all duration-1000 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <div
          v-for="(review, index) in mobileReviews"
          :key="index"
          class="rounded-3xl overflow-hidden transition-all duration-300">
          <img :src="review.image" :alt="`모바일 리뷰 ${index + 1}`" class="w-full h-auto object-cover" />
        </div>
      </div>

      <!-- 데스크톱: 무한 스크롤 (768px 이상) -->
      <div
        class="hidden md:block transition-all duration-1000 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'">
        <div class="max-w-6xl mx-auto overflow-hidden">
          <div class="scroll-container">
            <div
              ref="scrollContent"
              class="scroll-content"
              :class="{ paused: isDragging }"
              @mousedown="startDrag"
              @mousemove="onDrag"
              @mouseup="endDrag"
              @mouseleave="endDrag"
              @touchstart="startDrag"
              @touchmove="onDrag"
              @touchend="endDrag">
              <!-- 첫 번째 세트 -->
              <div v-for="(review, index) in desktopReviews" :key="`first-${index}`" class="scroll-item">
                <div class="rounded-4xl overflow-hidden transition-all duration-300">
                  <img
                    :src="review.image"
                    :alt="`데스크톱 리뷰 ${index + 1}`"
                    class="w-full h-full object-cover pointer-events-none select-none"
                    draggable="false" />
                </div>
              </div>
              <!-- 두 번째 세트 (무한 반복용) -->
              <div v-for="(review, index) in desktopReviews" :key="`second-${index}`" class="scroll-item">
                <div class="rounded-4xl overflow-hidden transition-all duration-300">
                  <img
                    :src="review.image"
                    :alt="`데스크톱 리뷰 ${index + 1}`"
                    class="w-full h-full object-cover pointer-events-none select-none"
                    draggable="false" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const isVisible = ref(false);
const isDragging = ref(false);
const startX = ref(0);
const scrollLeft = ref(0);
const scrollContent = ref(null);

let observer = null;

// 모바일용 리뷰 이미지
const mobileReviews = [
  { image: "/images/m_리뷰1.png" },
  { image: "/images/m_리뷰2.png" },
  { image: "/images/m_리뷰3.png" },
  { image: "/images/m_리뷰4.png" },
  { image: "/images/m_리뷰5.png" },
  { image: "/images/m_리뷰6.png" },
  { image: "/images/m_리뷰7.png" },
  { image: "/images/m_리뷰8.png" },
];

// 데스크톱용 리뷰 이미지
const desktopReviews = [
  { image: "/images/리뷰1.png" },
  { image: "/images/리뷰2.png" },
  { image: "/images/리뷰3.png" },
  { image: "/images/리뷰4.png" },
  { image: "/images/리뷰5.png" },
  { image: "/images/리뷰6.png" },
  { image: "/images/리뷰7.png" },
  { image: "/images/리뷰8.png" },
];

// 드래그 시작
const startDrag = (e) => {
  isDragging.value = true;
  const container = scrollContent.value.parentElement;
  startX.value = e.type.includes("mouse") ? e.pageX : e.touches[0].pageX;
  scrollLeft.value = container.scrollLeft;

  if (scrollContent.value) {
    scrollContent.value.style.cursor = "grabbing";
  }
};

// 드래그 중
const onDrag = (e) => {
  if (!isDragging.value) return;
  e.preventDefault();

  const container = scrollContent.value.parentElement;
  const x = e.type.includes("mouse") ? e.pageX : e.touches[0].pageX;
  const walk = (x - startX.value) * 2;
  container.scrollLeft = scrollLeft.value - walk;
};

// 드래그 종료
const endDrag = () => {
  isDragging.value = false;
  if (scrollContent.value) {
    scrollContent.value.style.cursor = "grab";
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

  const section = document.getElementById("review");
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

<style scoped>
.scroll-container {
  width: 100%;
  overflow-x: auto;
  overflow-y: hidden;
  padding: 20px 0;
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.scroll-container::-webkit-scrollbar {
  display: none;
}

.scroll-content {
  display: flex;
  gap: 10px;
  animation: scroll 50s linear infinite;
  width: fit-content;
  cursor: grab;
}

.scroll-content.paused {
  animation-play-state: paused;
}

.scroll-item {
  flex-shrink: 0;
  width: 270px;
}

@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

/* 드래그 중 선택 방지 */
.select-none {
  user-select: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}

.pointer-events-none {
  pointer-events: none;
}
</style>
