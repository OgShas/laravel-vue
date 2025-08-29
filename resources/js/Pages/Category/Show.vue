<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import { Head, Link } from '@inertiajs/vue3';

defineProps({
    category: Object
});
</script>

<template>
    <AppLayout>
        <Head :title="category.name" />
        <div class="container py-5">
            <h1>{{ category.name }}</h1>
            <img :src="category.image" class="img-fluid mb-3" alt="">
            <h3>Products</h3>
            <div class="row">
                <div v-for="product in category.products" :key="product.id" class="col-12 col-md-4 mb-3">
                    <div class="card">
                        <img :src="product.image" class="card-img-top" alt="">
                        <div class="card-body">
                            <h5>{{ product.name }}</h5>
                            <Link :href="`/products/${product.id}`" class="btn btn-primary btn-sm">View</Link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
