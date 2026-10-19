<script setup lang="ts">
import { Link } from '@inertiajs/vue3';
import AppLogoIcon from '@/components/AppLogoIcon.vue';
import { home } from '@/routes';

const { title = '', description = '' } = defineProps<{
    title?: string;
    description?: string;
}>();
</script>

<template>
    <div
        class="relative flex min-h-screen w-full items-center justify-center bg-cover bg-center bg-no-repeat p-4 sm:p-6"
        style="
            background-image: url('/images/pexels-codioful-7130481.jpg');
            font-family: 'Poppins', sans-serif;
        "
    >
        <!-- Background dark tint for readability -->
        <div class="absolute inset-0 bg-slate-950/40 backdrop-blur-[2px]"></div>

        <!-- Auth Card Container -->
        <div
            class="relative z-10 w-full max-w-[380px] rounded-xl border border-[#3c4964]/70 bg-[#252e42] p-7 text-white shadow-2xl"
        >
            <div class="mb-6 flex flex-col items-center">
                <Link
                    :href="home()"
                    class="mb-3 flex h-10 w-10 items-center justify-center rounded-lg border border-[#3c4964] bg-[#1a2233] transition-transform hover:scale-105"
                    title="Home"
                >
                    <AppLogoIcon class="size-6 fill-current text-white" />
                </Link>
                <h1
                    v-if="title"
                    class="text-center text-2xl font-semibold tracking-tight text-white"
                >
                    {{ title }}
                </h1>
                <p
                    v-if="description"
                    class="mt-1 text-center text-xs text-slate-300"
                >
                    {{ description }}
                </p>
            </div>

            <slot />
        </div>
    </div>
</template>
