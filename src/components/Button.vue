<template>
    <button 
        @click="$emit('btn-click')"
        class="btn"
        :style="{background: bg_color}"
        >
        {{ text }}
        <img :src="src" :alt="alt">
    </button>
</template>

<script>

    export default {
        name: 'Button',
        props: {
            text: {
                type: String,
                default: 'This is a button'
            },
            bg_color: 'white',
            src: '',
            alt: '',
        },
    }
</script>

<style lang="scss" scoped>
</style>