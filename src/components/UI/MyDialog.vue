<template>
    <div class="dialog" v-if="show" @click="hideDialog">
        <div class="dialog__content" @click.stop>
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: "MyDialog",
    props: {
        show: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideDialog() {
            this.$emit('update:show', false);
        }
    }
}
</script>

<style lang="sass">
.dialog
    position: fixed
    top: 0
    bottom: 0
    left: 0
    right: 0
    display: flex
    background: rgba(0, 0, 0, .5)
    
.dialog__content
    margin: auto
    padding: 20px
    background: white
    border-radius: 10px
    
</style>