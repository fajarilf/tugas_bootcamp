<template>
    <table class="table">
        <thead>
            <tr>
                <th>Name</th>
                <th>Qty</th>
                <th>Price</th>
                <th></th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(cartItem, index) in cart" :key="index">
                <td>{{ cartItem.item.Name }}</td>
                <td>
                    <button-component v-if="cartItem.quantity > 1" font="fa-solid fa-caret-left" model="btn btn-success"
                        value="false" @emitclicked="quantityMin(cartItem)" />
                    <button-component v-else font="fa-solid fa-caret-left" model="btn btn-secondary" />
                    {{ cartItem.quantity }}
                    <button-component v-if="cartItem.item.Stock > 0" font="fa-solid fa-caret-right" model="btn btn-success"
                        value="false" @emitclicked="quantityPlus(cartItem)" />
                    <button-component v-else font="fa-solid fa-caret-right" model="btn btn-secondary" />
                </td>
                <td>Rp. {{ cartItem.quantity * cartItem.item.Price }}</td>
                <!-- <td>
                    
                </td> -->
                <td>
                    <button-component font="fa-solid fa-trash-can" model="btn btn-danger" @emitclicked="remove(index)" />
                </td>
            </tr>
        </tbody>
    </table>
</template>
<script>
import buttonComponent from './buttonComponent.vue';
import formvalue from './formvalue.vue';
import { ref } from 'vue';
export default {
    components: {
        buttonComponent,
        formvalue
    },
    props: {
        cart: {},
    },
    methods: {
        remove(index) {
            const item = this.cart[index];
            item.item.Stock += item.quantity;
            this.cart.splice(index, 1);
            this.$emit('updateCart', this.cart)
        },
        quantityMin(cartItem) {
            cartItem.quantity -= 1;
            cartItem.item.Stock += 1;
            this.$emit('updateCart', this.cart)
        },
        quantityPlus(cartItem) {
            cartItem.quantity += 1;
            cartItem.item.Stock -= 1;
            this.$emit('updateCart', this.cart)
        },
    }
}
</script>