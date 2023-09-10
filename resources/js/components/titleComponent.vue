<template>
    <div :class="mainClass">
        <h1 :class="textclass">{{ text }}</h1>
    </div>
</template>

<script>
export default {
    props: {
        text: {
            type: String
        },
        mainClass: {
            type: String
        },
        textClass: {
            type: String
        }
    },
    mounted() {
        console.log('mounted');
    }
}
</script>