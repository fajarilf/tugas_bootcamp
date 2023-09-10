<template>
    <div class="container">
        <div>
            <title-component text="Semua Produk" mainClass="text-center" textClass="mt-3 mb-4"></title-component>
            <hr>
            <table-component :itemData="itemData" :fields="fields" @update="updateCart"></table-component>
        </div>
        <div>
            <title-component text="Keranjang Anda" mainClass="text-center" textClass="mt-3 mb-4"></title-component>
            <hr>
            <bottom-table :cart="cart" @update="updateCart"></bottom-table>
            <hr>
            <b>total price: Rp. {{ total }}</b>
            <hr>
            <button-component text="Checkout" model="btn btn-success" @emitclicked="checkout"></button-component>
        </div>
    </div>
</template>
<script>
import titleComponent from './titleComponent.vue';
import tableComponent from './tableComponent.vue';
import bottomTable from './bottomTable.vue';
import buttonComponent from './buttonComponent.vue';
import Swal from 'sweetalert2'
export default {
    components: {
        tableComponent,
        titleComponent,
        bottomTable,
        buttonComponent
    },
    data: function () {
        return {
            itemData: [
                { Name: "Indomie Goreng Rendang", Description: "Masakan instant terenak di dunia", Stock: 10, Price: 3900 },
                { Name: "Mie Gelas Rendang", Description: "Mie instant khusus anak kosan", Stock: 3, Price: 1500 },
                { Name: "Bakmi Mewah", Description: "Kalau anak kosan jangan macam2 deh", Stock: 80, Price: 10000 },
            ],
            fields: [
                'Name', 'Description', 'Stock', 'Price', 'Qty'
            ],
            cart: []
        }
    },
    computed: {
        total() {
            let total = 0;
            for (const cartItem of this.cart) {
                total += cartItem.quantity * cartItem.item.Price
            }
            return total
        }
    },
    methods: {
        updateCart(cart) {
            this.cart = cart
        },
        checkout() {
            // if (this.cart.length === 0) {
            //     alert("Keranjang mu kosong");
            //     return
            // }
            // alert(`Total: ${this.total}`);
            if (this.cart.length === 0) {
                Swal.fire({
                    title: 'Error!',
                    text: 'Keranjangmu Kosong',
                    icon: 'error',
                    confirmButtonText: 'Batal'
                })
            }
            else {
                Swal.fire({
                    title: 'Checkout',
                    text: `total: ${this.total}`,
                    icon: 'question',
                    showCancelButton: true,
                    confirmButtonColor: '#3085d6',
                    cancelButtonColor: '#d33',
                    confirmButtonText: 'Bayar'
                }).then((result) => {
                    if (result.isConfirmed) {
                        Swal.fire({
                            title: 'Success!',
                            text: 'Terima kasih telah berbelanja',
                            icon: 'success',
                        })
                    }
                })
            }
        }
    },
    mounted() {
        console.log('upperTable mounted');
    }
}
</script>