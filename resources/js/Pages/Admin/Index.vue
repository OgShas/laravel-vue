<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import { Head, usePage } from '@inertiajs/vue3';

// Get authenticated user data from Laravel Inertia shared props
const { auth } = usePage().props;
const user = auth.user; // admin info
</script>

<template>
    <AppLayout>
        <Head title="Admin Dashboard" />

        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Admin Dashboard</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 space-y-6">

                <!-- Welcome Box -->
                <div class="bg-white shadow-sm sm:rounded-lg p-6">
                    <h3 class="text-lg font-semibold mb-2">Welcome, {{ user.name }}</h3>
                    <p class="text-gray-700">You are logged in as <span class="font-medium">Admin</span>.</p>
                    <p class="text-gray-500 mt-1">Email: {{ user.email }}</p>
                </div>

                <!-- Example Stats (optional) -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="bg-white shadow-sm rounded-lg p-6 text-center">
                        <h3 class="text-gray-500">Total Users</h3>
                        <p class="text-2xl font-bold">120</p>
                    </div>
                    <div class="bg-white shadow-sm rounded-lg p-6 text-center">
                        <h3 class="text-gray-500">Posts</h3>
                        <p class="text-2xl font-bold">45</p>
                    </div>
                    <div class="bg-white shadow-sm rounded-lg p-6 text-center">
                        <h3 class="text-gray-500">Sales</h3>
                        <p class="text-2xl font-bold">300</p>
                    </div>
                </div>

            </div>
        </div>
    </AppLayout>
</template>
