<script setup lang="ts">
import { Form, Head, Link } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import { Spinner } from '@/components/ui/spinner';
import { register } from '@/routes';
import { store } from '@/routes/login';
import { request } from '@/routes/password';
import PasskeyVerify from '@/components/PasskeyVerify.vue';
import { Eye, EyeOff } from '@lucide/vue';
import { ref } from 'vue';

defineOptions({
    layout: {
        title: 'Login',
        description: '',
    },
});

defineProps<{
    status?: string;
    canResetPassword: boolean;
}>();

const showPassword = ref(false);
</script>

<template>
    <div class="w-full">
        <Head title="Log in" />

        <div
            v-if="status"
            class="mb-4 rounded-md border border-emerald-500/40 bg-emerald-950/80 p-2 text-center text-xs font-medium text-emerald-300"
        >
            {{ status }}
        </div>

        <PasskeyVerify class="mb-4" />

        <Form
            v-bind="store.form()"
            :reset-on-success="['password']"
            v-slot="{ errors, processing }"
            class="flex flex-col gap-4"
        >
            <div class="flex flex-col gap-4">
                <!-- Email -->
                <div>
                    <div
                        class="flex items-center rounded-md border border-[#3c4964] bg-[#1a2233] px-3 py-2.5 transition-colors focus-within:border-blue-500 focus-within:ring-1 focus-within:ring-blue-500"
                    >
                        <label
                            for="email"
                            class="mr-2.5 flex cursor-pointer items-center select-none"
                        >
                            <img
                                src="/images/person_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg"
                                alt="Email"
                                class="h-5 w-5 opacity-80"
                            />
                        </label>
                        <input
                            id="email"
                            type="email"
                            name="email"
                            required
                            v-focus
                            :tabindex="1"
                            autocomplete="email"
                            placeholder="Email"
                            class="w-full border-0 bg-transparent p-0 text-sm text-white placeholder:text-slate-400 focus:ring-0 focus:outline-none"
                        />
                    </div>
                    <InputError
                        :message="errors.email"
                        class="mt-1 text-xs text-rose-400"
                    />
                </div>

                <!-- Password -->
                <div>
                    <div
                        class="flex items-center rounded-md border border-[#3c4964] bg-[#1a2233] px-3 py-2.5 transition-colors focus-within:border-blue-500 focus-within:ring-1 focus-within:ring-blue-500"
                    >
                        <label
                            for="password"
                            class="mr-2.5 flex cursor-pointer items-center select-none"
                        >
                            <img
                                src="/images/lock_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg"
                                alt="Password"
                                class="h-5 w-5 opacity-80"
                            />
                        </label>
                        <input
                            id="password"
                            :type="showPassword ? 'text' : 'password'"
                            name="password"
                            required
                            :tabindex="2"
                            autocomplete="current-password"
                            placeholder="Password"
                            class="w-full border-0 bg-transparent p-0 text-sm text-white placeholder:text-slate-400 focus:ring-0 focus:outline-none"
                        />
                        <button
                            type="button"
                            @click="showPassword = !showPassword"
                            class="ml-2 cursor-pointer text-slate-400 transition-colors hover:text-white"
                            tabindex="-1"
                            :aria-label="
                                showPassword ? 'Hide password' : 'Show password'
                            "
                        >
                            <EyeOff v-if="showPassword" class="size-4" />
                            <Eye v-else class="size-4" />
                        </button>
                    </div>
                    <InputError
                        :message="errors.password"
                        class="mt-1 text-xs text-rose-400"
                    />
                </div>

                <!-- Remember me & Forgot Password -->
                <div
                    class="flex items-center justify-between text-xs text-slate-300"
                >
                    <label
                        for="remember"
                        class="flex cursor-pointer items-center gap-2 select-none"
                    >
                        <input
                            id="remember"
                            type="checkbox"
                            name="remember"
                            :tabindex="3"
                            class="h-4 w-4 rounded border-[#3c4964] bg-[#1a2233] text-blue-600 focus:ring-blue-500 focus:ring-offset-0"
                        />
                        <span>Remember me</span>
                    </label>
                    <Link
                        v-if="canResetPassword"
                        :href="request()"
                        class="text-blue-400 hover:text-blue-300 hover:underline"
                        :tabindex="5"
                    >
                        Forgot your password?
                    </Link>
                </div>

                <!-- Submit Button -->
                <button
                    type="submit"
                    class="mt-1 flex w-full cursor-pointer items-center justify-center gap-2 rounded-md bg-[#2563eb] py-3 text-sm font-medium text-white shadow-md transition-colors hover:bg-[#1d4ed8] disabled:cursor-not-allowed disabled:opacity-60"
                    :tabindex="4"
                    :disabled="processing"
                    data-test="login-button"
                >
                    <Spinner v-if="processing" class="size-4" />
                    <span>Login</span>
                </button>
            </div>

            <p class="mt-2 text-center text-xs text-slate-300">
                Don't have an account?
                <Link
                    :href="register()"
                    class="ml-1 font-medium text-blue-400 hover:text-blue-300 hover:underline"
                    :tabindex="6"
                >
                    Sign Up
                </Link>
            </p>
        </Form>
    </div>
</template>
