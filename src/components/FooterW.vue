<!-- components/Footer.vue -->
<template>
  <footer class="bg-black text-white py-12 md:py-16">
    <div class="container mx-auto px-4">
      <div class="text-center flex flex-col items-center">
        <!-- 로고 -->
        <img src="/images/logo.png" alt="STUDYforME Logo" class="h-4 mb-10" />

        <!-- 회사 정보 -->
        <div class="text-gray-400 text-sm mb-6">
          <p>
            대표: 김미리 <br class="block md:hidden" />
            <span class="hidden md:block"> | </span>회사명 : (주)스터디포미
          </p>
          <p>사업자등록번호 : 755-86-03232</p>
        </div>

        <!-- 저작권 및 이용약관 -->
        <div class="text-gray-400 text-sm space-y-2 mb-6">
          <div class="flex flex-wrap justify-center gap-2 md:gap-4">
            <a
              href="https://sform.notion.site/89d7dd52bad94ef8b14e8230178a0aeb"
              target="_blank"
              class="hover:text-purple-400 transition-colors duration-300">
              개인정보 처리방침
            </a>
            <span class="text-gray-700">|</span>
            <a
              href="https://sform.notion.site/d7bef64871d341c191d858971d45ced6"
              target="_blank"
              class="hover:text-purple-400 transition-colors duration-300">
              이용약관
            </a>
          </div>
          <!-- <p class="mt-4 text-gray-500">© 2024 STUDYforME. All rights reserved.</p> -->
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
// 필요한 경우 추가 로직
</script>
