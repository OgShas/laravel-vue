<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import {Head, Link} from "@inertiajs/vue3";

defineProps({
    products: Array
});
</script>

<template>
    <AppLayout>
        <Head title="All Products"/>

        <div class="container py-5">
            <h1 class="mb-4">All Products</h1>

            <div class="row">
                <div
                    v-for="product in products"
                    :key="product.id"
                    class="col-12 col-md-4 mb-4"
                >
                    <div class="card h-100">
                        <img
                            v-if="product.image"
                            :src="product.image"
                            class="card-img-top"
                            alt="Product image"
                        >
                        <div class="card-body">
                            <h5 class="card-title">{{ product.name }}</h5>
                            <p class="card-text">{{ product.description }}</p>
                            <p class="fw-bold">$ {{ product.price }}</p>

                            <!-- Link to product show page -->
                            <Link
                                :href="route('products.show', product.id)"
                                class="btn btn-primary"
                            >
                                View Details
                            </Link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
