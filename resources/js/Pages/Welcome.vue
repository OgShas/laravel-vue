<script setup>
import { Head, Link } from '@inertiajs/vue3';
import AppLayout from "@/Layouts/AppLayout.vue";

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    laravelVersion: { type: String, required: true },
    phpVersion: { type: String, required: true },
    products: Array,
    categories: Array,
});
</script>

<template>
    <AppLayout>
        <Head title="Welcome" />

        <!-- Categories Section -->
        <div class="container py-5">
            <h2 class="mb-4 text-center">Categories</h2>
            <div class="row">
                <div v-for="category in categories" :key="category.id" class="col-12 col-md-4 mb-4">
                    <div class="card h-100 shadow-sm">
                        <div class="card-body text-center d-flex flex-column justify-content-between">
                            <img :src="category.image" class="mb-3 mx-auto rounded-circle"
                                 style="height:120px; width:120px; object-fit:cover;" alt="Category Image">
                            <h5 class="card-title">{{ category.name }}</h5>
                            <Link :href="`/categories/${category.id}`" class="btn btn-primary btn-sm mt-3">
                                View
                            </Link>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Products Section -->
        <div class="container py-5">
            <h2 class="mb-4 text-center">All Products</h2>
            <div class="row">
                <div v-for="product in products" :key="product.id" class="col-12 col-md-4 mb-4">
                    <div class="card h-100 shadow-sm">
                        <img :src="product.image" class="card-img-top" style="height:200px; object-fit:cover;" alt="Product Image">
                        <div class="card-body d-flex flex-column justify-content-between">
                            <h5 class="card-title">{{ product.name }}</h5>
                            <p class="card-text">{{ product.description }}</p>
                        </div>
                        <div class="card-footer d-flex justify-content-between align-items-center">
                            <span class="fw-bold">${{ product.price }}</span>
                            <Link :href="`/products/${product.id}`" class="btn btn-primary btn-sm">
                                View
                            </Link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
