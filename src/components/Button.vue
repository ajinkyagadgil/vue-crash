<template>
    <!-- <button v-on:click="onBtnClick()" class="btn" :style="{background:color}">{{text}}</button> -->
    <!-- instead of v-on:click we can use @click -->
    <button @click="onBtnClick()" class="btn" :style="{background:color}">{{text}}</button>
</template>

<script>
    export default {
        name:'Button',
        props: {
            text: String,
            color: String
        },
        methods: {
            onBtnClick(){
                this.$emit('btn-click')
            }
        }
    }
</script>
