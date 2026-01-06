<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)
const sectionRef = ref(null)
const activeTab = ref('experience')

const experiences = [
    {
        company: 'iFAST Global Hub AI',
        role: 'IT Specialist',
        period: 'Jul 2024 - Present',
        description: 'Working on AI and technology solutions at a leading fintech company.',
        highlights: [],
        current: true,
    },
    {
        company: 'Maybank',
        role: 'Digital Banking, Delivery & Operations Intern',
        period: 'Jan 2024 - Apr 2024',
        description: 'Contributed to digital banking initiatives at Malaysia\'s largest bank.',
        highlights: [
            'Frontend development using React, Tailwind CSS, and in-house frameworks',
            'Backend training with Java Spring Boot and MySQL microservices',
            'Performed logging aspects, JUnit testing, and automated testing via Katalon',
            'Cloud computing with AWS EC2 instances and Nginx',
        ],
    },
    {
        company: 'Growth Charger',
        role: 'Software Engineer & Programme Executive',
        period: 'Jun 2023 - Dec 2023',
        description: 'Led end-to-end platform development at a startup accelerator.',
        highlights: [
            'Built platform from scratch to prototype in 2 months using Next.js 13, Tailwind CSS, and Supabase',
            'Led a team of 2 engineers from prototype to production',
            'Designed user journeys with emphasis on minimal and efficient UI/UX',
            'Co-organized events including InnoJam design challenge by Cyberview',
        ],
    },
    {
        company: 'Crabee',
        role: 'Social Media Content Creator & Operations',
        period: 'Jun 2021 - Jul 2022',
        description: 'Digital growth and operations for an e-commerce platform.',
        highlights: [
            'Overhauled company website design to enhance user experience',
            'Achieved 10% social media growth through strategic content',
        ],
    },
]

const education = [
    {
        institution: 'Sunway University',
        degree: 'Bachelor of Computer Science (Hons)',
        period: '2021 - 2024',
        details: 'CGPA: 3.68',
        activities: ['Sunway Tech Club Member', 'Mixed Martial Arts Club Committee'],
    },
    {
        institution: "Taylor's University",
        degree: 'Foundation in Natural and Built Environment',
        period: '2019 - 2020',
        details: 'CGPA: 3.17',
        activities: [],
    },
    {
        institution: 'SMK Seafield',
        degree: 'SPM',
        period: '2014 - 2018',
        details: '9A',
        activities: [],
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
        { threshold: 0.1 }
    )

    if (sectionRef.value) {
        observer.observe(sectionRef.value)
    }
})
</script>

<template>
    <section
        ref="sectionRef"
        id="experience"
        class="section-padding bg-[#F9F9F9] relative overflow-hidden"
    >
        <!-- Background pattern -->
        <div class="absolute inset-0 opacity-50">
            <div class="absolute top-20 left-20 w-72 h-72 bg-white rounded-full blur-3xl"></div>
            <div class="absolute bottom-20 right-20 w-96 h-96 bg-[#FF6969]/5 rounded-full blur-3xl"></div>
        </div>

        <div class="max-w-6xl mx-auto relative z-10">
            <!-- Section header -->
            <div
                class="flex items-center gap-4 mb-12 transition-all duration-700"
                :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
            >
                <span class="font-roboto text-sm text-[#FF6969] tracking-widest">02</span>
                <h2 class="font-visuelt text-4xl md:text-5xl font-bold">Experience & Education</h2>
                <div class="flex-1 h-px bg-gray-300 ml-4"></div>
            </div>

            <!-- Tab navigation -->
            <div
                class="flex gap-1 mb-12 p-1 bg-white rounded-full w-fit shadow-sm transition-all duration-700 delay-200"
                :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
            >
                <button
                    @click="activeTab = 'experience'"
                    class="px-6 py-2 rounded-full font-roboto text-sm transition-all duration-300"
                    :class="activeTab === 'experience' ? 'bg-[#FF6969] text-white' : 'text-gray-600 hover:text-gray-900'"
                >
                    Experience
                </button>
                <button
                    @click="activeTab = 'education'"
                    class="px-6 py-2 rounded-full font-roboto text-sm transition-all duration-300"
                    :class="activeTab === 'education' ? 'bg-[#FF6969] text-white' : 'text-gray-600 hover:text-gray-900'"
                >
                    Education
                </button>
            </div>

            <!-- Experience Timeline -->
            <div v-show="activeTab === 'experience'" class="relative">
                <!-- Timeline line -->
                <div class="absolute left-0 md:left-8 top-0 bottom-0 w-px bg-gray-200"></div>

                <div class="space-y-8">
                    <div
                        v-for="(exp, index) in experiences"
                        :key="exp.company"
                        class="relative pl-8 md:pl-20 transition-all duration-700"
                        :style="{ transitionDelay: `${300 + index * 150}ms` }"
                        :class="isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-4'"
                    >
                        <!-- Timeline dot -->
                        <div
                            class="absolute left-0 md:left-8 top-2 -translate-x-1/2 w-3 h-3 rounded-full border-2 transition-colors duration-300"
                            :class="exp.current ? 'bg-[#FF6969] border-[#FF6969]' : 'bg-white border-gray-300 hover:border-[#FF6969]'"
                        ></div>

                        <!-- Current indicator -->
                        <div
                            v-if="exp.current"
                            class="absolute left-0 md:left-8 top-2 -translate-x-1/2 w-3 h-3 rounded-full bg-[#FF6969] animate-ping"
                        ></div>

                        <!-- Card -->
                        <div class="bg-white rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow duration-300 group">
                            <div class="flex flex-col md:flex-row md:items-start md:justify-between gap-2 mb-3">
                                <div>
                                    <div class="flex items-center gap-3">
                                        <h3 class="font-visuelt text-xl font-bold group-hover:text-[#FF6969] transition-colors">
                                            {{ exp.company }}
                                        </h3>
                                        <span
                                            v-if="exp.current"
                                            class="px-2 py-0.5 bg-[#FF6969]/10 text-[#FF6969] text-xs rounded-full font-roboto"
                                        >
                                            Current
                                        </span>
                                    </div>
                                    <p class="font-roboto text-gray-600">{{ exp.role }}</p>
                                </div>
                                <span class="font-roboto text-sm text-gray-400 whitespace-nowrap">
                                    {{ exp.period }}
                                </span>
                            </div>

                            <p class="font-roboto text-gray-500 text-sm mb-4">{{ exp.description }}</p>

                            <ul v-if="exp.highlights.length" class="space-y-2">
                                <li
                                    v-for="highlight in exp.highlights"
                                    :key="highlight"
                                    class="flex items-start gap-2 font-roboto text-sm text-gray-600"
                                >
                                    <span class="w-1.5 h-1.5 bg-[#FF6969] rounded-full mt-1.5 flex-shrink-0"></span>
                                    {{ highlight }}
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Education Timeline -->
            <div v-show="activeTab === 'education'" class="relative">
                <!-- Timeline line -->
                <div class="absolute left-0 md:left-8 top-0 bottom-0 w-px bg-gray-200"></div>

                <div class="space-y-8">
                    <div
                        v-for="(edu, index) in education"
                        :key="edu.institution"
                        class="relative pl-8 md:pl-20 transition-all duration-700"
                        :style="{ transitionDelay: `${300 + index * 150}ms` }"
                        :class="isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-4'"
                    >
                        <!-- Timeline dot -->
                        <div
                            class="absolute left-0 md:left-8 top-2 -translate-x-1/2 w-3 h-3 rounded-full bg-white border-2 border-gray-300 hover:border-[#FF6969] transition-colors duration-300"
                        ></div>

                        <!-- Card -->
                        <div class="bg-white rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow duration-300 group">
                            <div class="flex flex-col md:flex-row md:items-start md:justify-between gap-2 mb-3">
                                <div>
                                    <h3 class="font-visuelt text-xl font-bold group-hover:text-[#FF6969] transition-colors">
                                        {{ edu.institution }}
                                    </h3>
                                    <p class="font-roboto text-gray-600">{{ edu.degree }}</p>
                                </div>
                                <span class="font-roboto text-sm text-gray-400 whitespace-nowrap">
                                    {{ edu.period }}
                                </span>
                            </div>

                            <div class="flex items-center gap-4">
                                <span class="px-3 py-1 bg-gray-100 rounded-full text-sm font-roboto text-gray-700">
                                    {{ edu.details }}
                                </span>
                            </div>

                            <div v-if="edu.activities.length" class="mt-4 pt-4 border-t border-gray-100">
                                <p class="font-roboto text-xs text-gray-400 mb-2 uppercase tracking-wider">Activities</p>
                                <div class="flex flex-wrap gap-2">
                                    <span
                                        v-for="activity in edu.activities"
                                        :key="activity"
                                        class="px-2 py-1 bg-[#FF6969]/5 text-[#FF6969] text-xs rounded font-roboto"
                                    >
                                        {{ activity }}
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
