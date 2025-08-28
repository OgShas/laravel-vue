<script setup>
import { Head, Link } from '@inertiajs/vue3';
import AppLayout from "@/Layouts/AppLayout.vue";

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    laravelVersion: { type: String, required: true },
    phpVersion: { type: String, required: true },
    products: Array
});
</script>

<template>
    <AppLayout>
        <Head title="Welcome" />

        <!-- Products section -->
        <div class="container py-5">
            <h1 class="mb-4 text-center">All Products</h1>

            <div class="row">
                <div v-for="product in products" :key="product.id" class="col-md-4 mb-4">
                    <div class="card h-100">
                        <img :src="product.image" class="card-img-top" alt="Product Image">
                        <div class="card-body">
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
