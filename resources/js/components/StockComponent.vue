<template>
    <section class="container-fluid mt-4">
        <h2 class="h2">Semua Barang</h2>
        <table class="table">
            <thead>
                <tr>
                    <th scope="col">Name</th>
                    <th scope="col">Description</th>
                    <th scope="col">Stock</th>
                    <th scope="col">Price</th>
                    <th scope="col"></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in stockItems" :key="item.id">
                    <td>{{ item.name }}</td>
                    <td>{{ item.description }}</td>
                    <td>{{ item.stock }}</td>
                    <td>Rp. {{ item.price }}</td>
                    <td><button class="btn btn-primary" :class="{ disabled: item.stock === 0 }" @click="addToCart(item.id, item.name, item.price)">Add to cart</button></td>
                </tr>
            </tbody>
        </table>
    </section>
</template>

<script>
    export default {
        emits: ['emit-addToCart'],
        props: {
            stockItems: {
                type: Array,
                default() {
                    return [];
                }
            }
        },
        methods: {
            addToCart(id, nama, price) {
                this.$emit('emit-addToCart', id, nama, price);
            }
        }
    }
</script>

<style>

</style>
