<template>
    <div class="min-h-screen bg-dark">
        <HeroBackground />

        <!-- Add a general navigation bar -->
        <CommonHeader />

        <main class="relative z-10">
            <!-- Core content block -->
            <section class="h-screen flex items-center">
                <div class="container mx-auto px-6 text-center">
                    <h1
                        class="text-5xl md:text-7xl font-bold text-white mb-6"
                        ref="title"
                    >
                        Warehouse&nbsp;Management&nbsp;System
                    </h1>
                    <p class="text-xl text-gray-300 mb-8" ref="subtitle">
                        Produced by the 4-idots group
                    </p>
                </div>
            </section>

            <!-- Add a universal footer -->
            <footer class="bg-zinc-700 py-12">
                <div class="container mx-auto px-6">
                    <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                        <!-- Company Information -->
                        <div class="mb-8 md:mb-0">
                            <h3 class="text-white text-xl font-bold mb-4"
                                >4-idots</h3
                            >
                            <p class="text-gray-400 text-sm">
                                A whole new kind of web page
                            </p>
                        </div>

                        <!-- Quick link -->
                        <div>
                            <h4 class="text-white font-semibold mb-4"
                                >Quick Links</h4
                            >
                            <ul class="space-y-2">
                                <li>
                                    <NuxtLink
                                        class="text-gray-400 hover:text-white text-sm transition-colors"
                                        >About Us</NuxtLink
                                    >
                                </li>
                                <li>
                                    <NuxtLink
                                        class="text-gray-400 hover:text-white text-sm transition-colors"
                                        >Research</NuxtLink
                                    >
                                </li>
                                <li>
                                    <NuxtLink
                                        class="text-gray-400 hover:text-white text-sm transition-colors"
                                        >Careers</NuxtLink
                                    >
                                </li>
                            </ul>
                        </div>

                        <!-- Contact information -->
                        <div>
                            <h4 class="text-white font-semibold mb-4"
                                >Contact</h4
                            >
                            <ul class="space-y-2">
                                <li class="text-gray-400 text-sm"
                                    >404@notfound.com</li
                                >
                                <li class="text-gray-400 text-sm"
                                    >(400) 8823-823</li
                                >
                                <li class="text-gray-400 text-sm"
                                    >CRAZY THURSDAY VME50</li
                                >
                            </ul>
                        </div>

                        <!-- Social media -->
                        <div>
                            <h4 class="text-white font-semibold mb-4"
                                >Follow Us</h4
                            >
                            <div class="flex space-x-4">
                                <a
                                    href="#"
                                    class="text-gray-400 hover:text-white transition-colors"
                                >
                                    <Icon name="uil:linkedin" class="w-6 h-6" />
                                </a>
                                <a
                                    href="#"
                                    class="text-gray-400 hover:text-white transition-colors"
                                >
                                    <Icon name="uil:twitter" class="w-6 h-6" />
                                </a>
                                <a
                                    href="#"
                                    class="text-gray-400 hover:text-white transition-colors"
                                >
                                    <Icon name="uil:youtube" class="w-6 h-6" />
                                </a>
                            </div>
                        </div>
                    </div>

                    <!-- Copyright information -->
                    <div class="border-t border-dark-600 mt-12 pt-8">
                        <p class="text-gray-500 text-center text-sm">
                            &copy; 2025 4-idots. All rights reserved.
                        </p>
                    </div>
                </div>
            </footer>
        </main>
    </div>
</template>

<script setup lang="ts">
// Navigation data
import HeroBackground from "~/components/Home/HeroBackground.vue";
import CommonHeader from "~/components/Common/Header.vue";

const navLinks = [
    { title: "About", path: "/about" },
    { title: "Login", path: "/login" },
    { title: "Signup", path: "/signup" },
];

// Function card data
const features = [
    {
        title: "AI-Driven Strategies",
        description:
            "Machine learning models trained on alternative data sources",
    },
    {
        title: "Global Reach",
        description: "Operating in 15+ countries with localized strategies",
    },
    {
        title: "Risk Management",
        description: "Real-time portfolio optimization and monitoring",
    },
];

import { ref, onMounted } from "vue";

// The animation code of Step 3 should be placed here ▼
const title = ref(null); // In the corresponding template <h1 ref="title">
const subtitle = ref(null); // In the corresponding template <p ref="subtitle">

onMounted(() => {
    // Typing effect loop animation
    const text = title.value.innerText; // Obtain the original text
    title.value.innerText = ""; // Clear the text

    const typewriterEffect = (text, index = 0) => {
        if (index < text.length) {
            // If it is a space character, display the space directly
            if (text.charAt(index) === " ") {
                title.value.innerText += " "; // Keep Spaces
            } else {
                title.value.innerText += text.charAt(index); // Typing
            }
            index++;
            setTimeout(() => typewriterEffect(text, index), 100); // Add one character every 100ms
        } else {
            // Loop play
            setTimeout(() => {
                title.value.innerText = ""; // Clear the text
                typewriterEffect(text); // Restart the typing effect
            }, 2000); // Start again in 2 seconds
        }
    };

    // Activate the typing effect
    typewriterEffect(text);
});
</script>
