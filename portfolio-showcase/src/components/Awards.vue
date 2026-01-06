<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)
const sectionRef = ref(null)

const awards = [
    {
        title: 'Hong Leong Bank "Can You Hack It"',
        year: '2022',
        achievement: 'Champion',
        color: 'bg-yellow-500',
        icon: '🏆',
        description: 'First place in the national hackathon competition organized by Hong Leong Bank.',
    },
    {
        title: 'Malaysia TechLympics Data Science Challenge',
        year: '2023',
        achievement: 'Top 3',
        color: 'bg-gray-400',
        icon: '🥈',
        description: 'Placed among the top 3 teams in the national data science competition.',
    },
    {
        title: 'Standard Chartered Bank "Impact Hack"',
        year: '2023',
        achievement: 'Finalist',
        color: 'bg-amber-700',
        icon: '🥉',
        description: 'Selected as a finalist in the Standard Chartered Bank hackathon.',
    },
]

onMounted(() => {
    const observer = new IntersectionObserver(
        (entries) => {
            entries.forEach((entry) => {
                if (entry.isIntersecting) {
                    isVisible.value = true
                }
            })
        },
        { threshold: 0.2 }
    )

    if (sectionRef.value) {
        observer.observe(sectionRef.value)
    }
})
</script>

<template>
    <section
        ref="sectionRef"
        id="awards"
        class="section-padding bg-white relative overflow-hidden"
    >
        <!-- Background decoration -->
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-[#FF6969]/5 rounded-full blur-3xl"></div>

        <div class="max-w-6xl mx-auto relative z-10">
            <!-- Section header -->
            <div
                class="flex items-center gap-4 mb-16 transition-all duration-700"
                :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
            >
                <span class="font-roboto text-sm text-[#FF6969] tracking-widest">03</span>
                <h2 class="font-visuelt text-4xl md:text-5xl font-bold">Awards & Achievements</h2>
                <div class="flex-1 h-px bg-gray-200 ml-4"></div>
            </div>

            <!-- Awards grid -->
            <div class="grid md:grid-cols-3 gap-6">
                <div
                    v-for="(award, index) in awards"
                    :key="award.title"
                    class="group relative transition-all duration-700"
                    :style="{ transitionDelay: `${200 + index * 150}ms` }"
                    :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
                >
                    <!-- Card -->
                    <div class="h-full bg-gray-50 rounded-2xl p-6 hover:bg-white hover:shadow-xl transition-all duration-500 border border-transparent hover:border-gray-100">
                        <!-- Trophy icon with gradient background -->
                        <div class="w-16 h-16 rounded-xl bg-gradient-to-br from-[#FF6969] to-[#ff8a8a] flex items-center justify-center mb-6 group-hover:scale-110 transition-transform duration-300">
                            <span class="text-3xl">{{ award.icon }}</span>
                        </div>

                        <!-- Achievement badge -->
                        <div class="flex items-center gap-2 mb-3">
                            <span class="px-3 py-1 bg-[#FF6969] text-white text-xs font-roboto font-bold rounded-full">
                                {{ award.achievement }}
                            </span>
                            <span class="font-roboto text-sm text-gray-400">{{ award.year }}</span>
                        </div>

                        <!-- Title -->
                        <h3 class="font-visuelt text-lg font-bold mb-2 group-hover:text-[#FF6969] transition-colors">
                            {{ award.title }}
                        </h3>

                        <!-- Description -->
                        <p class="font-roboto text-sm text-gray-500 leading-relaxed">
                            {{ award.description }}
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
