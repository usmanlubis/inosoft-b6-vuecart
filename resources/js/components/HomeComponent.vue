<template>
    <main class="container">
        <stock-component :stockItems="stockItems" @emit-addToCart="addToCart"></stock-component>
        <cart-component :cartItems="cartItems" :totalPrice="totalPrice" @emit-deleteCartItem="deleteCartItem"></cart-component>
        <div class="container">
            <button class="btn btn-success" @click="checkout">Checkout</button>
        </div>
    </main>
</template>

<script>
    export default {
        data() {
            return {
                stockItems: [
                    {
                        id: 1,
                        name: 'Indomie Goreng Rendang',
                        description: 'Masakan instant terenak di dunia',
                        stock: 10,
                        price: 3900
                    },
                    {
                        id: 2,
                        name: 'Mie Goreng Rendang',
                        description: 'Masakan instant khusus anak kostan',
                        stock: 5,
                        price: 1500
                    },
                    {
                        id: 3,
                        name: 'Bakmi Mewah',
                        description: 'Kalau anak kostan jangan macam-macam deh',
                        stock: 80,
                        price: 10000
                    }
                ],
                cartItems: []
            }
        },
        computed: {
            totalPrice() {
                let sum = 0;
                for(let item of this.cartItems) { sum = sum + (item.price * item.quantity); }
                return sum;
            }
        },
        methods: {
            addToCart(id, name, price) {
                if (this.cartItems.some((item) => item.id === id)) {
                    this.cartItems.map((item) => {
                        if (item.id === id) {
                            item.quantity++;
                            this.stockItems.map((item) => {
                                if(item.id === id){
                                    item.stock--;
                                }
                            });
                        }
                    })
                } else {
                    this.stockItems.map((item) => {
                        if(item.id === id){
                            item.stock--;
                        }
                    })
                    const newItem = {
                        id,
                        name,
                        quantity: 1,
                        price,
                    };
                    this.cartItems.push(newItem);
                }
            },
            deleteCartItem(id){
                this.cartItems.map((item) => {
                    if (item.id === id) {
                        item.quantity--;
                    }
                })
                this.stockItems.map((item) => {
                    if(item.id === id){
                        item.stock++;
                    }
                })
            },
            checkout() {
                return alert(`Pay us Rp. ${this.totalPrice}`);
            }
        }
    }
</script>
