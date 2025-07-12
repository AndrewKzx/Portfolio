<script setup>
import SplitFlap from '@/components/SplitFlap.vue'
import { ref, onMounted, onUnmounted } from 'vue'

// For parallax on scroll
defineProps()
const scrollY = ref(0)
const handleScroll = () => {
    scrollY.value = window.scrollY
}
onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
    <!-- Container with a gray background and dot-grid pattern -->
    <header class="hero bg-[#F9F9F9] h-156 relative py-16 px-8 overflow-hidden">
        <div class="absolute inset-0 flex items-center justify-center">
            <!-- Parallax circles -->
            <div class="relative" :style="{
                transform: `translateY(${scrollY * 0.05}px)`
            }">
                <!-- White circle (slower parallax) -->
                <div class="bg-white w-120 h-120 rounded-full"
                    :style="{ transform: `translateY(${scrollY * 0.02}px)` }"></div>

                <!-- Red circle (faster parallax) -->
                <div class="bg-[#FF6969] w-64 h-64 rounded-full absolute bottom-20 right-0 translate-x-1/4"
                    :style="{ transform: `translateY(${scrollY * 0.1}px)` }"></div>
            </div>

            <!-- Glassmorphism card overlay -->
            <div class="glass-card absolute top-1/2 right-1/4 p-6 rounded-lg z-20">
                <p class="text-base font-roboto">"Code. Design. Iterate."</p>
            </div>
        </div>

        <!-- Texts in foreground -->
        <div class="relative z-30 max-w-xl mt-40 ml-74">
            <h1 class="font-visuelt text-6xl font-bold mb-1">Andrew</h1>
            <h2 class="font-visuelt text-4xl mb-4">Khor Zun Xiong</h2>
            <p class="font-roboto text-base">
                Software Engineer &nbsp;|&nbsp; Hackathoner &nbsp;|&nbsp; Malaysia
            </p>
        </div>

        <div class="relative z-30 mt-40 ml-74 flex font-roboto text-sm">
            <a href="https://github.com/AndrewKzx" target="_blank" class="underline">Github</a>
            <p>&nbsp;/&nbsp;</p>
            <a href="https://www.linkedin.com/in/andrewkhorzx/" target="_blank" class="underline">LinkedIn</a>
        </div>
    </header>
</template>

<style scoped>
.hero {
    /* subtle dot-grid background */
    background-image: radial-gradient(circle, rgba(0, 0, 0, 0.02) 1px, transparent 1px);
    background-size: 20px 20px;
}

.glass-card {
    background: rgba(255, 255, 255, 0.2);
    backdrop-filter: blur(8px);
    border: 1px solid rgba(255, 255, 255, 0.3);
    max-width: 200px;
    text-align: center;
}
</style>
