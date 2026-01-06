<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const activeSection = ref('')
const isMobileMenuOpen = ref(false)

const navItems = [
    { name: 'About', href: '#about' },
    { name: 'Experience', href: '#experience' },
    { name: 'Awards', href: '#awards' },
    { name: 'Contact', href: '#contact' },
]

const handleScroll = () => {
    isScrolled.value = window.scrollY > 50

    // Update active section based on scroll position
    const sections = ['about', 'experience', 'awards', 'contact']
    const scrollPosition = window.scrollY + 100

    for (const section of sections) {
        const element = document.getElementById(section)
        if (element) {
            const offsetTop = element.offsetTop
            const offsetHeight = element.offsetHeight

            if (scrollPosition >= offsetTop && scrollPosition < offsetTop + offsetHeight) {
                activeSection.value = section
                break
            }
        }
    }

    // If at the top, no section is active
    if (window.scrollY < 100) {
        activeSection.value = ''
    }
}

const scrollToSection = (href) => {
    isMobileMenuOpen.value = false
    const element = document.querySelector(href)
    if (element) {
        element.scrollIntoView({ behavior: 'smooth' })
    }
}

const scrollToTop = () => {
    window.scrollTo({ top: 0, behavior: 'smooth' })
}

onMounted(() => {
    window.addEventListener('scroll', handleScroll)
    handleScroll()
})

onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
    <nav
        class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
        :class="isScrolled ? 'bg-white/90 backdrop-blur-md shadow-sm' : 'bg-transparent'"
    >
        <div class="max-w-6xl mx-auto px-6 py-4">
            <div class="flex items-center justify-between">
                <!-- Logo/Name -->
                <button
                    @click="scrollToTop"
                    class="font-visuelt text-xl font-bold transition-colors duration-300 hover:text-[#FF6969]"
                    :class="isScrolled ? 'text-gray-900' : 'text-gray-900'"
                >
                    AK<span class="text-[#FF6969]">.</span>
                </button>

                <!-- Desktop Navigation -->
                <div class="hidden md:flex items-center gap-8">
                    <button
                        v-for="item in navItems"
                        :key="item.name"
                        @click="scrollToSection(item.href)"
                        class="relative font-roboto text-sm transition-colors duration-300 group"
                        :class="[
                            isScrolled ? 'text-gray-600 hover:text-gray-900' : 'text-gray-600 hover:text-gray-900',
                            activeSection === item.href.slice(1) ? 'text-[#FF6969]' : ''
                        ]"
                    >
                        {{ item.name }}
                        <!-- Active indicator -->
                        <span
                            class="absolute -bottom-1 left-0 h-0.5 bg-[#FF6969] transition-all duration-300"
                            :class="activeSection === item.href.slice(1) ? 'w-full' : 'w-0 group-hover:w-full'"
                        ></span>
                    </button>

                    <!-- Resume button -->
                    <a
                        href="#contact"
                        @click.prevent="scrollToSection('#contact')"
                        class="px-4 py-2 bg-[#FF6969] text-white text-sm font-roboto rounded-full hover:bg-[#ff5252] transition-all duration-300 hover:shadow-md"
                    >
                        Get in Touch
                    </a>
                </div>

                <!-- Mobile menu button -->
                <button
                    @click="isMobileMenuOpen = !isMobileMenuOpen"
                    class="md:hidden p-2 rounded-lg hover:bg-gray-100 transition-colors"
                    :class="isScrolled ? 'text-gray-900' : 'text-gray-900'"
                >
                    <svg
                        v-if="!isMobileMenuOpen"
                        class="w-6 h-6"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                    >
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
                    </svg>
                    <svg
                        v-else
                        class="w-6 h-6"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                    >
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                    </svg>
                </button>
            </div>
        </div>

        <!-- Mobile menu -->
        <div
            class="md:hidden overflow-hidden transition-all duration-300 bg-white/95 backdrop-blur-md"
            :class="isMobileMenuOpen ? 'max-h-80 border-t border-gray-100' : 'max-h-0'"
        >
            <div class="px-6 py-4 space-y-1">
                <button
                    v-for="item in navItems"
                    :key="item.name"
                    @click="scrollToSection(item.href)"
                    class="block w-full text-left px-4 py-3 font-roboto text-gray-600 hover:text-[#FF6969] hover:bg-gray-50 rounded-lg transition-colors"
                    :class="activeSection === item.href.slice(1) ? 'text-[#FF6969] bg-[#FF6969]/5' : ''"
                >
                    {{ item.name }}
                </button>
                <a
                    href="#contact"
                    @click.prevent="scrollToSection('#contact')"
                    class="block w-full text-center mt-4 px-4 py-3 bg-[#FF6969] text-white font-roboto rounded-full hover:bg-[#ff5252] transition-colors"
                >
                    Get in Touch
                </a>
            </div>
        </div>
    </nav>
</template>
