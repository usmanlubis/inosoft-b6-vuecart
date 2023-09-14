<template>
    <section class="container-fluid my-4">
        <h2 class="h2">Keranjang Belanja</h2>
            <table class="table">
                <thead>
                    <tr>
                        <th scope="col">Name</th>
                        <th scope="col">Quantity</th>
                        <th scope="col">Price</th>
                        <th scope="col"></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in cartItems" :key="item.id">
                    <template v-if="item.quantity">
                        <td>{{ item.name }}</td>
                        <td>{{ item.quantity }}</td>
                        <td>Rp. {{ item.price }}</td>
                        <td><button class="btn btn-danger" @click="deleteCartItem(item.id)">Delete</button></td>
                    </template>
                    </tr>
                    <tr>
                        <th scope="row">Total</th>
                        <td></td>
                        <td class="fw-bold">RP. {{ totalPrice }}</td>
                        <td></td>
                    </tr>
                </tbody>
            </table>
    </section>
</template>

<script>
    export default {
        emits: ['emit-deleteCartItem'],
        props: {
            cartItems: {
                type: Array,
                default() {
                    return [];
                }
            },
            totalPrice: {
                type: Number,
                default() {
                    return 0;
                }
            }
        },
        methods: {
            deleteCartItem(id){
                this.$emit('emit-deleteCartItem', id);
            }
        }
    }
</script>

<style>

</style>
