<script setup>
import { ref } from "vue";
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import Dropdown from "@/Components/Dropdown.vue";
import DropdownLink from "@/Components/DropdownLink.vue";
import NavLink from "@/Components/NavLink.vue";
import ResponsiveNavLink from "@/Components/ResponsiveNavLink.vue";
import { Link } from "@inertiajs/vue3";

const showingNavigationDropdown = ref(false);
</script>

<template>
    <div class="min-h-screen flex flex-col bg-gray-100">
        <!-- Header -->
        <nav class="bg-white border-b border-gray-200 shadow">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between h-16">
                    <!-- Left side -->
                    <div class="flex items-center">
                        <Link :href="route('dashboard')" class="flex items-center">
                            <ApplicationLogo class="h-9 w-auto text-indigo-600" />
                            <span class="ml-2 font-bold text-gray-800 text-lg">My App</span>
                        </Link>

                        <!-- Navigation Links (example) -->
                        <div class="hidden sm:flex sm:space-x-6 ml-10">
                            <NavLink :href="route('dashboard')" :active="route().current('dashboard')">
                                Dashboard
                            </NavLink>
                        </div>
                    </div>

                    <!-- Right side -->
                    <div class="hidden sm:flex sm:items-center">
                        <div v-if="$page.props.auth?.user" class="ml-3 relative">
                            <!-- Authenticated Dropdown -->
                            <Dropdown align="right" width="48">
                                <template #trigger>
                                    <button
                                        type="button"
                                        class="inline-flex items-center px-3 py-2 border border-transparent
                                               text-sm font-medium rounded-md text-gray-700 hover:text-indigo-600
                                               focus:outline-none transition"
                                    >
                                        {{ $page.props.auth.user.name }}
                                        <svg class="ml-2 h-4 w-4" fill="currentColor" viewBox="0 0 20 20">
                                            <path
                                                fill-rule="evenodd"
                                                d="M5.293 7.293a1 1 0 011.414 0L10
                                                   10.586l3.293-3.293a1 1 0
                                                   111.414 1.414l-4 4a1 1 0
                                                   01-1.414 0l-4-4a1 1 0
                                                   010-1.414z"
                                                clip-rule="evenodd"
                                            />
                                        </svg>
                                    </button>
                                </template>
                                <template #content>
                                    <DropdownLink :href="route('profile.edit')">Profile</DropdownLink>
                                    <DropdownLink :href="route('logout')" method="post" as="button">
                                        Log Out
                                    </DropdownLink>
                                </template>
                            </Dropdown>
                        </div>

                        <!-- Guest buttons -->
                        <div v-else class="flex space-x-4">
                            <Link
                                :href="route('login')"
                                class="px-4 py-2 text-sm font-semibold text-indigo-600
                                       border border-indigo-600 rounded-lg hover:bg-indigo-50"
                            >
                                Log in
                            </Link>
                            <Link
                                :href="route('register')"
                                class="px-4 py-2 text-sm font-semibold text-white bg-indigo-600
                                       rounded-lg hover:bg-indigo-700"
                            >
                                Register
                            </Link>
                        </div>
                    </div>

                    <!-- Mobile Hamburger -->
                    <div class="-mr-2 flex items-center sm:hidden">
                        <button
                            @click="showingNavigationDropdown = !showingNavigationDropdown"
                            class="inline-flex items-center justify-center p-2 rounded-md
                                   text-gray-400 hover:text-gray-600 hover:bg-gray-100 focus:outline-none"
                        >
                            <svg class="h-6 w-6" stroke="currentColor" fill="none" viewBox="0 0 24 24">
                                <path
                                    :class="{ hidden: showingNavigationDropdown, 'inline-flex': !showingNavigationDropdown }"
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="M4 6h16M4 12h16M4 18h16"
                                />
                                <path
                                    :class="{ hidden: !showingNavigationDropdown, 'inline-flex': showingNavigationDropdown }"
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="M6 18L18 6M6 6l12 12"
                                />
                            </svg>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Mobile Menu -->
            <div :class="{ block: showingNavigationDropdown, hidden: !showingNavigationDropdown }" class="sm:hidden">
                <div class="pt-2 pb-3 space-y-1">
                    <ResponsiveNavLink :href="route('dashboard')" :active="route().current('dashboard')">
                        Dashboard
                    </ResponsiveNavLink>
                </div>

                <!-- Authenticated -->
                <div v-if="$page.props.auth?.user" class="pt-4 pb-1 border-t border-gray-200">
                    <div class="px-4">
                        <div class="font-medium text-base text-gray-800">{{ $page.props.auth.user.name }}</div>
                        <div class="font-medium text-sm text-gray-500">{{ $page.props.auth.user.email }}</div>
                    </div>
                    <div class="mt-3 space-y-1">
                        <ResponsiveNavLink :href="route('profile.edit')">Profile</ResponsiveNavLink>
                        <ResponsiveNavLink :href="route('logout')" method="post" as="button">
                            Log Out
                        </ResponsiveNavLink>
                    </div>
                </div>

                <!-- Guest -->
                <div v-else class="pt-4 pb-1 border-t border-gray-200 space-y-1">
                    <ResponsiveNavLink :href="route('login')">Log in</ResponsiveNavLink>
                    <ResponsiveNavLink :href="route('register')">Register</ResponsiveNavLink>
                </div>
            </div>
        </nav>

        <!-- Page Content -->
        <main class="flex-grow">
            <slot />
        </main>

        <!-- Footer -->
        <footer class="bg-gray-200 text-center p-4 mt-6">
            &copy; {{ new Date().getFullYear() }} My App
        </footer>
    </div>
</template>
