<template>
    <table class="table">
        <thead>
            <tr>
                <th v-for="field in fields" :key="field">{{ field }}</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in itemData" :key="item">
                <!-- <td v-for="field in fields" :key="field">{{ item[field] }}</td> -->
                <td>{{ item.Name }}</td>
                <td>{{ item.Description }}</td>
                <td>{{ item.Stock }}</td>
                <td>Rp. {{ item.Price }}</td>
                <td>
                    <button-component v-if="item.Stock" font="fa-solid fa-cart-shopping" model="btn btn-success"
                        @emitclicked="addToCart(item)"></button-component>
                    <button-component v-else font="fa-solid fa-cart-shopping" model="btn btn-secondary"></button-component>
                </td>
            </tr>
        </tbody>
    </table>
</template>
<script>
import buttonComponent from './buttonComponent.vue';
import bottomTable from './bottomTable.vue';
export default {
    components: {
        buttonComponent,
        bottomTable
        // valueComponent
    },
    data() {
        return {
            cart: []
        }
    },
    props: {
        itemData: {
            type: Array,
        },
        fields: {
            type: Array,
        }
    },
    methods: {
        addToCart(item) {
            const product = this.cart.find(product => product.item.Name === item.Name);
            if (product) {
                product.quantity += 1;
                item.Stock -= 1;
            } else {
                this.cart.push({ item, quantity: 1 });
                item.Stock -= 1;
            }
            this.$emit('update', this.cart)
        }
    },
    mounted() {
        console.log('table mounted')
    }
}
</script>