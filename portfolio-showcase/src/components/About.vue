<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)
const sectionRef = ref(null)

const skills = [
    { category: 'Languages', items: ['Java', 'Python', 'SQL', 'JavaScript'] },
    { category: 'Frontend', items: ['React.js', 'Next.js', 'Tailwind CSS', 'HTML/CSS'] },
    { category: 'Backend', items: ['Java Spring Boot', 'Reflex', 'JavaFX'] },
    { category: 'Databases', items: ['MySQL', 'Supabase', 'Upstash Redis'] },
    { category: 'Tools', items: ['Git', 'AWS EC2', 'Nginx', 'Adobe Suite'] },
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
        id="about"
        class="section-padding bg-white relative overflow-hidden"
    >
        <!-- Background decoration -->
        <div class="absolute top-0 right-0 w-96 h-96 bg-[#FF6969]/5 rounded-full -translate-y-1/2 translate-x-1/2"></div>
        <div class="absolute bottom-0 left-0 w-64 h-64 bg-gray-100 rounded-full translate-y-1/2 -translate-x-1/2"></div>

        <div class="max-w-6xl mx-auto relative z-10">
            <!-- Section header -->
            <div
                class="flex items-center gap-4 mb-16 transition-all duration-700"
                :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
            >
                <span class="font-roboto text-sm text-[#FF6969] tracking-widest">01</span>
                <h2 class="font-visuelt text-4xl md:text-5xl font-bold">About Me</h2>
                <div class="flex-1 h-px bg-gray-200 ml-4"></div>
            </div>

            <div class="grid md:grid-cols-2 gap-16">
                <!-- Left column - Bio -->
                <div
                    class="transition-all duration-700 delay-200"
                    :class="isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-8'"
                >
                    <p class="font-roboto text-gray-600 text-lg leading-relaxed mb-6">
                        I'm a Computer Science fresh graduate from Sunway University with hands-on experience
                        in software engineering. I enjoy building digital products that solve real problems
                        and create meaningful impact.
                    </p>
                    <p class="font-roboto text-gray-600 text-lg leading-relaxed mb-6">
                        My journey includes internships at major institutions like Maybank where I worked
                        on digital banking solutions, and startup experience at Growth Charger where I led
                        platform development from scratch to production.
                    </p>
                    <p class="font-roboto text-gray-600 text-lg leading-relaxed mb-8">
                        When I'm not coding, you'll find me participating in hackathons—where I've won
                        competitions like the Hong Leong Bank "Can You Hack It" challenge—or contributing
                        to tech communities.
                    </p>

                    <!-- Quick facts -->
                    <div class="grid grid-cols-2 gap-4">
                        <div class="p-4 bg-gray-50 rounded-lg">
                            <p class="font-visuelt text-2xl font-bold text-[#FF6969]">3+</p>
                            <p class="font-roboto text-sm text-gray-500">Years Coding</p>
                        </div>
                        <div class="p-4 bg-gray-50 rounded-lg">
                            <p class="font-visuelt text-2xl font-bold text-[#FF6969]">3</p>
                            <p class="font-roboto text-sm text-gray-500">Hackathon Awards</p>
                        </div>
                        <div class="p-4 bg-gray-50 rounded-lg">
                            <p class="font-visuelt text-2xl font-bold text-[#FF6969]">3.68</p>
                            <p class="font-roboto text-sm text-gray-500">CGPA</p>
                        </div>
                        <div class="p-4 bg-gray-50 rounded-lg">
                            <p class="font-visuelt text-2xl font-bold text-[#FF6969]">3</p>
                            <p class="font-roboto text-sm text-gray-500">Internships</p>
                        </div>
                    </div>
                </div>

                <!-- Right column - Skills -->
                <div
                    class="transition-all duration-700 delay-400"
                    :class="isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-8'"
                >
                    <h3 class="font-visuelt text-xl font-bold mb-6">Technical Skills</h3>

                    <div class="space-y-6">
                        <div
                            v-for="(skillGroup, index) in skills"
                            :key="skillGroup.category"
                            class="transition-all duration-500"
                            :style="{ transitionDelay: `${500 + index * 100}ms` }"
                            :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
                        >
                            <p class="font-roboto text-sm text-gray-400 mb-2 uppercase tracking-wider">
                                {{ skillGroup.category }}
                            </p>
                            <div class="flex flex-wrap gap-2">
                                <span
                                    v-for="skill in skillGroup.items"
                                    :key="skill"
                                    class="px-3 py-1.5 bg-gray-100 rounded-full text-sm font-roboto text-gray-700 hover:bg-[#FF6969] hover:text-white transition-colors cursor-default"
                                >
                                    {{ skill }}
                                </span>
                            </div>
                        </div>
                    </div>

                    <!-- Languages -->
                    <div
                        class="mt-8 pt-6 border-t border-gray-100 transition-all duration-500"
                        :style="{ transitionDelay: '900ms' }"
                        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
                    >
                        <p class="font-roboto text-sm text-gray-400 mb-3 uppercase tracking-wider">Languages</p>
                        <div class="flex gap-4">
                            <div class="flex items-center gap-2">
                                <span class="w-2 h-2 bg-[#FF6969] rounded-full"></span>
                                <span class="font-roboto text-sm">English</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <span class="w-2 h-2 bg-[#FF6969] rounded-full"></span>
                                <span class="font-roboto text-sm">Mandarin</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <span class="w-2 h-2 bg-[#FF6969] rounded-full"></span>
                                <span class="font-roboto text-sm">Bahasa Melayu</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
