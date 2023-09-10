<template>
    <!-- <button type="button" @click="clicked" :class="model">{{ text }}</button> -->
    <input type="text" @keyup.enter="typed" style="width: auto;" :value="itemValue" />
</template>
<script>
export default {
    props: {
        itemValue: {
            type: Number,
        },
    },
    methods: {
        typed() {
            this.$emit('emittyped')
        }
    }
}
</script>