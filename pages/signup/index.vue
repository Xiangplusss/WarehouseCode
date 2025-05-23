<template>
    <div
        class="min-h-screen relative overflow-hidden flex items-center justify-center"
    >
        <CommonHeader />
        <!-- Dynamic gradient background -->
        <div
            class="absolute inset-0 z-0 animate-gradient-move bg-gradient-to-r from-[#0f172a] via-[#1e293b] to-[#000000] gradient-bg"
        ></div>

        <!-- Registration form -->
        <div
            class="relative z-10 backdrop-blur-md bg-white/10 rounded-xl shadow-2xl p-8 w-96 border border-white/20"
        >
            <h2 class="text-3xl font-bold text-white mb-8 text-center"
                >User Registration</h2
            >

            <form @submit.prevent="handleSubmit">
                <!-- Email input -->
                <div class="mb-6">
                    <label class="block text-white mb-2 text-xl font-semibold"
                        >Email</label
                    >
                    <input
                        v-model="form.email"
                        type="email"
                        required
                        class="w-full px-4 py-2 bg-white/10 border border-white/20 rounded-lg focus:ring-2 focus:ring-blue-500 outline-none text-white placeholder-white/50"
                        :class="{ 'border-red-500': errors.email }"
                        placeholder="Please enter email"
                    />
                    <p v-if="errors.email" class="text-red-300 text-sm mt-1">{{
                        errors.email
                    }}</p>
                </div>

                <!-- Password input -->
                <div class="mb-6">
                    <label class="block text-white mb-2 text-xl font-semibold"
                        >Password</label
                    >
                    <input
                        v-model="form.password"
                        type="password"
                        required
                        class="w-full px-4 py-2 bg-white/10 border border-white/20 rounded-lg focus:ring-2 focus:ring-blue-500 outline-none text-white placeholder-white/50"
                        :class="{ 'border-red-500': errors.password }"
                        placeholder="Please enter password"
                    />
                    <p
                        v-if="errors.password"
                        class="text-red-300 text-sm mt-1"
                        >{{ errors.password }}</p
                    >
                </div>

                <!-- Confirm password -->
                <div class="mb-6">
                    <label class="block text-white mb-2 text-xl font-semibold"
                        >Confirm password</label
                    >
                    <input
                        v-model="form.confirmPassword"
                        type="password"
                        required
                        class="w-full px-4 py-2 bg-white/10 border border-white/20 rounded-lg focus:ring-2 focus:ring-blue-500 outline-none text-white placeholder-white/50"
                        :class="{ 'border-red-500': errors.confirmPassword }"
                        placeholder="Please enter password again"
                    />
                    <p
                        v-if="errors.confirmPassword"
                        class="text-red-300 text-sm mt-1"
                        >{{ errors.confirmPassword }}</p
                    >
                </div>

                <!-- Name input -->
                <div class="mb-6">
                    <label class="block text-white mb-2 text-xl font-semibold"
                        >Name</label
                    >
                    <input
                        v-model="form.name"
                        type="text"
                        required
                        class="w-full px-4 py-2 bg-white/10 border border-white/20 rounded-lg focus:ring-2 focus:ring-blue-500 outline-none text-white placeholder-white/50"
                        :class="{ 'border-red-500': errors.name }"
                        placeholder="Please enter name"
                    />
                    <p v-if="errors.name" class="text-red-300 text-sm mt-1">{{
                        errors.name
                    }}</p>
                </div>

                <!-- Upload the avatar -->
                <div class="mb-8">
                    <label class="block text-white mb-2 text-xl font-semibold"
                        >Upload your profile picture</label
                    >
                    <div class="flex items-center space-x-4">
                        <div
                            class="relative w-16 h-16 rounded-full overflow-hidden border-2 border-dashed border-white/20 bg-white/10"
                        >
                            <img
                                v-if="avatarPreview"
                                :src="avatarPreview"
                                class="w-full h-full object-cover"
                            />
                            <input
                                type="file"
                                accept="image/png, image/jpeg"
                                @change="handleAvatarUpload"
                                class="absolute inset-0 opacity-0 cursor-pointer"
                            />
                        </div>
                        <span class="text-sm text-white/50"
                            >only support PNG/JPG format</span
                        >
                    </div>
                    <p v-if="errors.avatar" class="text-red-300 text-sm mt-1">{{
                        errors.avatar
                    }}</p>
                </div>

                <button
                    type="submit"
                    class="w-full bg-white/20 text-white py-3 rounded-lg hover:bg-white/30 transition-colors border border-white/20"
                >
                    Register
                </button>

                <div class="mt-4 text-center">
                    <router-link
                        to="/login"
                        class="text-white/70 hover:text-white transition-colors"
                    >
                        Already have an account? Login now.
                    </router-link>
                </div>
            </form>
        </div>

        <!-- Success prompt -->
        <transition name="fade">
            <div
                v-if="showSuccess"
                class="fixed top-4 right-4 bg-green-500/80 backdrop-blur-md text-white px-6 py-3 rounded-lg shadow-lg flex items-center z-20 border border-white/20"
            >
                <svg
                    class="w-5 h-5 mr-2"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                >
                    <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M5 13l4 4L19 7"
                    />
                </svg>
                Registration Successful!
            </div>
        </transition>
    </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";
import CommonHeader from "~/components/Common/Header.vue";

const router = useRouter();

// Form data
const form = ref({
    email: "",
    password: "",
    confirmPassword: "",
    name: "",
    avatar: null,
});

// Verification error
const errors = ref({
    email: "",
    password: "",
    confirmPassword: "",
    name: "",
    avatar: "",
});

// Avatar preview
const avatarPreview = ref(null);
const showSuccess = ref(false);

// Avatar upload processing
const handleAvatarUpload = (e: Event) => {
    const target = e.target as HTMLInputElement;
    const file = target.files?.[0];
    if (!file) return;

    // Verify the file type
    if (!["image/jpeg", "image/png"].includes(file.type)) {
        errors.value.avatar = "Only JPG/PNG format is supported";
        return;
    }

    // Generate a preview image
    const reader = new FileReader();
    reader.onload = (e) => {
        if (e.target?.result) {
            avatarPreview.value = e.target.result;
            form.value.avatar = file;
            errors.value.avatar = "";
        }
    };
    reader.readAsDataURL(file);
};

// Form submission
const handleSubmit = () => {
    // Reset the error message
    errors.value = {
        email: "",
        password: "",
        confirmPassword: "",
        name: "",
        avatar: "",
    };

    // Email verification
    if (!/^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(form.value.email)) {
        errors.value.email = "The mailbox is incorrectly formatted";
    }

    // Password verification
    if (form.value.password.length < 6) {
        errors.value.password = "The password must be at least 6 characters long";
    }

    // Confirm password verification
    if (form.value.password !== form.value.confirmPassword) {
        errors.value.confirmPassword = "The password entered twice is inconsistent";
    }

    // Name verification
    if (form.value.name.trim().length < 2) {
        errors.value.name = "The name needs to be at least 2 characters";
    }

    // Avatar verification
    if (!form.value.avatar) {
        errors.value.avatar = "Please upload a profile picture";
    }

    // Submission logic
    if (!Object.values(errors.value).some((e) => e)) {
        showSuccess.value = true;
        setTimeout(() => {
            router.push("/login");
        }, 2000);
    }
};
</script>

<style>
/* Dynamic gradient animation */
.gradient-bg {
    background-size: 200% 200%;
    animation: gradient-move 8s ease-in-out infinite;
}
@keyframes gradient-move {
    0% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
    }
}

.fade-enter-active,
.fade-leave-active {
    transition: all 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
    transform: translateX(100%);
}

/* The input box is automatically filled with styles */
input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus {
    -webkit-text-fill-color: white;
    -webkit-box-shadow: 0 0 0px 1000px rgba(255, 255, 255, 0.1) inset;
    transition: background-color 5000s ease-in-out 0s;
}
</style>
