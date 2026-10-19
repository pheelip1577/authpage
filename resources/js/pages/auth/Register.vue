<script setup lang="ts">
import { Form, Head, Link } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import { Spinner } from '@/components/ui/spinner';
import { login } from '@/routes';
import { store } from '@/routes/register';
import { Eye, EyeOff } from '@lucide/vue';
import { ref } from 'vue';

defineProps<{
    passwordRules?: string;
}>();

defineOptions({
    layout: {
        title: 'Create Account',
        description: '',
    },
});

const showPassword = ref(false);
const showConfirmPassword = ref(false);
</script>

<template>
    <div class="w-full">
        <Head title="Register" />

        <Form
            v-bind="store.form()"
            :reset-on-success="['password', 'password_confirmation']"
            v-slot="{ errors, processing }"
            class="flex flex-col gap-4"
        >
            <div class="flex flex-col gap-3.5">
                <!-- Name -->
                <div>
                    <div
                        class="flex items-center rounded-md border border-[#3c4964] bg-[#1a2233] px-3 py-2.5 transition-colors focus-within:border-blue-500 focus-within:ring-1 focus-within:ring-blue-500"
                    >
                        <label
                            for="name"
                            class="mr-2.5 flex cursor-pointer items-center select-none"
                        >
                            <img
                                src="/images/person_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg"
                                alt="Name"
                                class="h-5 w-5 opacity-80"
                            />
                        </label>
                        <input
                            id="name"
                            type="text"
                            name="name"
                            required
                            v-focus
                            :tabindex="1"
                            autocomplete="name"
                            placeholder="Full Name"
                            class="w-full border-0 bg-transparent p-0 text-sm text-white placeholder:text-slate-400 focus:ring-0 focus:outline-none"
                        />
                    </div>
                    <InputError
                        :message="errors.name"
                        class="mt-1 text-xs text-rose-400"
                    />
                </div>

                <!-- Email -->
                <div>
                    <div
                        class="flex items-center rounded-md border border-[#3c4964] bg-[#1a2233] px-3 py-2.5 transition-colors focus-within:border-blue-500 focus-within:ring-1 focus-within:ring-blue-500"
                    >
                        <label
                            for="email"
                            class="mr-2.5 flex w-5 items-center justify-center font-medium text-slate-300 select-none"
                        >
                            <span>@</span>
                        </label>
                        <input
                            id="email"
                            type="email"
                            name="email"
                            required
                            :tabindex="2"
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
                            :tabindex="3"
                            autocomplete="new-password"
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

                <!-- Confirm Password -->
                <div>
                    <div
                        class="flex items-center rounded-md border border-[#3c4964] bg-[#1a2233] px-3 py-2.5 transition-colors focus-within:border-blue-500 focus-within:ring-1 focus-within:ring-blue-500"
                    >
                        <label
                            for="password_confirmation"
                            class="mr-2.5 flex cursor-pointer items-center select-none"
                        >
                            <img
                                src="/images/lock_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg"
                                alt="Confirm Password"
                                class="h-5 w-5 opacity-80"
                            />
                        </label>
                        <input
                            id="password_confirmation"
                            :type="showConfirmPassword ? 'text' : 'password'"
                            name="password_confirmation"
                            required
                            :tabindex="4"
                            autocomplete="new-password"
                            placeholder="Confirm Password"
                            class="w-full border-0 bg-transparent p-0 text-sm text-white placeholder:text-slate-400 focus:ring-0 focus:outline-none"
                        />
                        <button
                            type="button"
                            @click="showConfirmPassword = !showConfirmPassword"
                            class="ml-2 cursor-pointer text-slate-400 transition-colors hover:text-white"
                            tabindex="-1"
                            :aria-label="
                                showConfirmPassword
                                    ? 'Hide password'
                                    : 'Show password'
                            "
                        >
                            <EyeOff v-if="showConfirmPassword" class="size-4" />
                            <Eye v-else class="size-4" />
                        </button>
                    </div>
                    <InputError
                        :message="errors.password_confirmation"
                        class="mt-1 text-xs text-rose-400"
                    />
                </div>

                <!-- Submit Button -->
                <button
                    type="submit"
                    class="mt-1.5 flex w-full cursor-pointer items-center justify-center gap-2 rounded-md bg-[#2563eb] py-3 text-sm font-medium text-white shadow-md transition-colors hover:bg-[#1d4ed8] disabled:cursor-not-allowed disabled:opacity-60"
                    :tabindex="5"
                    :disabled="processing"
                    data-test="register-user-button"
                >
                    <Spinner v-if="processing" class="size-4" />
                    <span>Sign Up</span>
                </button>
            </div>

            <p class="mt-2 text-center text-xs text-slate-300">
                Already have an account?
                <Link
                    :href="login()"
                    class="ml-1 font-medium text-blue-400 hover:text-blue-300 hover:underline"
                    :tabindex="6"
                >
                    Log In
                </Link>
            </p>
        </Form>
    </div>
</template>
