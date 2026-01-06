<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isLoaded = ref(false)

onMounted(() => {
    setTimeout(() => {
        isLoaded.value = true
    }, 100)
})
</script>

<template>
    <header class="hero bg-[#F9F9F9] min-h-screen relative py-16 px-8 overflow-hidden flex items-center">
        <!-- Dot grid background -->
        <div class="absolute inset-0 dot-grid"></div>

        <!-- Comfort zone circle - positioned so content "steps out" of it -->
        <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
            <!-- Main comfort zone circle -->
            <div
                class="comfort-zone absolute rounded-full border-2 border-gray-200 transition-all duration-1000"
                :class="isLoaded ? 'opacity-100 scale-100' : 'opacity-0 scale-90'"
            ></div>

            <!-- Inner dashed circle - the boundary being crossed -->
            <div
                class="comfort-zone-inner absolute rounded-full border border-dashed border-gray-300 transition-all duration-1000 delay-200"
                :class="isLoaded ? 'opacity-60 scale-100' : 'opacity-0 scale-95'"
            ></div>

            <!-- Accent element outside the zone - representing the leap -->
            <div
                class="absolute w-4 h-4 bg-[#FF6969] rounded-full transition-all duration-700 delay-700 accent-dot"
                :class="isLoaded ? 'opacity-100 scale-100' : 'opacity-0 scale-0'"
            ></div>
        </div>

        <!-- Main content -->
        <div class="relative z-30 w-full px-8 md:px-16 lg:px-24">
            <div class="max-w-4xl">
                <!-- Greeting -->
                <p
                    class="font-roboto text-sm tracking-[0.3em] text-gray-400 mb-8 uppercase transition-all duration-700"
                    :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
                >
                    Hello, I'm
                </p>

                <!-- Name - ANDREW (solid) -->
                <div class="overflow-hidden">
                    <h1
                        class="font-visuelt text-7xl md:text-8xl lg:text-9xl font-bold leading-[0.9] tracking-tight transition-all duration-700 delay-100"
                        :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-full'"
                    >
                        ANDREW
                    </h1>
                </div>

                <!-- Name - KHOR (outline) -->
                <div class="overflow-hidden mt-2">
                    <h1
                        class="name-outline font-visuelt text-7xl md:text-8xl lg:text-9xl font-bold leading-[0.9] tracking-tight transition-all duration-700 delay-200"
                        :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-full'"
                    >
                        KHOR
                    </h1>
                </div>

                <!-- Animated line -->
                <div
                    class="h-1 bg-[#FF6969] mt-8 mb-10 transition-all duration-1000 delay-500 origin-left"
                    :class="isLoaded ? 'w-32' : 'w-0'"
                ></div>

                <!-- Role - simplified text -->
                <p
                    class="font-roboto text-gray-500 text-base md:text-lg tracking-wide mb-8 transition-all duration-700 delay-400"
                    :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
                >
                    Software Engineer · Hackathon Champion · Malaysia
                </p>

                <!-- Description -->
                <p
                    class="font-roboto text-gray-600 max-w-lg mb-12 leading-relaxed text-base md:text-lg transition-all duration-700 delay-500"
                    :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
                >
                    Computer Science graduate from Sunway University with a passion for building
                    impactful software solutions and winning hackathons.
                </p>

                <!-- Social links -->
                <div
                    class="flex items-center gap-6 transition-all duration-700 delay-600"
                    :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
                >
                    <a
                        href="https://github.com/AndrewKzx"
                        target="_blank"
                        class="group flex items-center gap-2 font-roboto text-sm hover:text-[#FF6969] transition-colors"
                    >
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                        </svg>
                        <span class="group-hover:underline">GitHub</span>
                    </a>
                    <span class="text-gray-300">|</span>
                    <a
                        href="https://www.linkedin.com/in/andrew-khor-zun-xiong-470353197/"
                        target="_blank"
                        class="group flex items-center gap-2 font-roboto text-sm hover:text-[#FF6969] transition-colors"
                    >
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                        </svg>
                        <span class="group-hover:underline">LinkedIn</span>
                    </a>
                    <span class="text-gray-300">|</span>
                    <a
                        href="mailto:khorz01@gmail.com"
                        class="group flex items-center gap-2 font-roboto text-sm hover:text-[#FF6969] transition-colors"
                    >
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
                        </svg>
                        <span class="group-hover:underline">Email</span>
                    </a>
                </div>
            </div>
        </div>

        <!-- Scroll indicator -->
        <div
            class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 transition-all duration-700 delay-800"
            :class="isLoaded ? 'opacity-100' : 'opacity-0'"
        >
            <span class="font-roboto text-xs text-gray-400 tracking-widest">SCROLL</span>
            <div class="w-px h-8 bg-gray-300 animate-pulse"></div>
        </div>
    </header>
</template>

<style scoped>
.hero {
    background-color: #F9F9F9;
}

.dot-grid {
    background-image: radial-gradient(circle, rgba(0, 0, 0, 0.03) 1px, transparent 1px);
    background-size: 24px 24px;
}

.name-outline {
    color: transparent;
    -webkit-text-stroke: 2px #1a1a1a;
    text-stroke: 2px #1a1a1a;
}

/* Comfort zone circles - positioned to the right so content "steps out" to the left */
.comfort-zone {
    width: 500px;
    height: 500px;
    right: 10%;
    transform: translateX(20%);
}

.comfort-zone-inner {
    width: 400px;
    height: 400px;
    right: 10%;
    transform: translateX(20%);
}

/* Red accent dot - outside the comfort zone, representing the leap forward */
.accent-dot {
    right: calc(10% + 280px);
    top: 30%;
}

@media (max-width: 1024px) {
    .comfort-zone {
        width: 400px;
        height: 400px;
        right: 5%;
    }
    .comfort-zone-inner {
        width: 320px;
        height: 320px;
        right: 5%;
    }
    .accent-dot {
        right: calc(5% + 220px);
    }
}

@media (max-width: 768px) {
    .comfort-zone {
        width: 300px;
        height: 300px;
        right: -10%;
        top: 20%;
    }
    .comfort-zone-inner {
        width: 240px;
        height: 240px;
        right: -10%;
        top: 20%;
    }
    .accent-dot {
        right: calc(-10% + 180px);
        top: 15%;
    }
}
</style>
