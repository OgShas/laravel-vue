<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import { Head } from '@inertiajs/vue3';

defineProps({
    product: Object
});
</script>

<template>
    <AppLayout>
        <Head :title="product.name" />
        <div class="container py-5">
            <h1>{{ product.name }}</h1>
            <img :src="product.image" class="img-fluid mb-3" alt="">
            <p>{{ product.description }}</p>
            <p><strong>Price:</strong> ${{ product.price }}</p>
        </div>
    </AppLayout>
</template>
