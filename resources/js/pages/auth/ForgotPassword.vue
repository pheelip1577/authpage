<script setup lang="ts">
import { Form, Head, Link } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import { Spinner } from '@/components/ui/spinner';
import { login } from '@/routes';
import { email } from '@/routes/password';

defineOptions({
    layout: {
        title: 'Forgot Password',
        description: 'Enter your email to receive a password reset link',
    },
});

defineProps<{
    status?: string;
}>();
</script>

<template>
    <div class="w-full">
        <Head title="Forgot password" />

        <div
            v-if="status"
            class="mb-4 rounded-md border border-emerald-500/40 bg-emerald-950/80 p-2 text-center text-xs font-medium text-emerald-300"
        >
            {{ status }}
        </div>

        <Form v-bind="email.form()" v-slot="{ errors, processing }" class="flex flex-col gap-4">
            <div>
                <div class="flex items-center rounded-md border border-[#3c4964] bg-[#1a2233] px-3 py-2.5 transition-colors focus-within:border-blue-500 focus-within:ring-1 focus-within:ring-blue-500">
                    <label for="email" class="mr-2.5 flex w-5 items-center justify-center font-medium text-slate-300 select-none">
                        <span>@</span>
                    </label>
                    <input
                        id="email"
                        type="email"
                        name="email"
                        autocomplete="off"
                        required
                        v-focus
                        placeholder="Email"
                        class="w-full border-0 bg-transparent p-0 text-sm text-white placeholder:text-slate-400 focus:outline-none focus:ring-0"
                    />
                </div>
                <InputError :message="errors.email" class="mt-1 text-xs text-rose-400" />
            </div>

            <button
                type="submit"
                class="mt-1 flex w-full cursor-pointer items-center justify-center gap-2 rounded-md bg-[#2563eb] py-3 text-sm font-medium text-white shadow-md transition-colors hover:bg-[#1d4ed8] disabled:cursor-not-allowed disabled:opacity-60"
                :disabled="processing"
                data-test="email-password-reset-link-button"
            >
                <Spinner v-if="processing" class="size-4" />
                <span>Email password reset link</span>
            </button>

            <p class="mt-2 text-center text-xs text-slate-300">
                Or, return to
                <Link
                    :href="login()"
                    class="ml-1 font-medium text-blue-400 hover:text-blue-300 hover:underline"
                >
                    Log In
                </Link>
            </p>
        </Form>
    </div>
</template>
