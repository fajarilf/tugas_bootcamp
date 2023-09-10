<template>
    <button type="button" @click="clicked" :class="model"><i :class="font">{{ text }}</i></button>
</template>
<script>
export default {
    props: {
        text: {
            type: String,
        },
        model: {
            type: String
        },
        font: {
            type: String
        }
    },
    methods: {
        clicked() {
            this.$emit('emitclicked')
        }
    }
}
</script>