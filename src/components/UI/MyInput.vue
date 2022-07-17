<template>
    <input
      class="input"
      type="text"
      :value="modelValue"
      @input="updateInput"
    />
</template>

<script>
export default {
    name: "MyInput",
    props: {
        modelValue: [String, Number]
    },
    methods: {
        updateInput(e) {
            this.$emit('update:modelValue', e.target.value)
        }
    }
}
</script>

<style lang="sass">
.input
    box-sizing: border-box
    width: 100%
    padding: 10px 15px
    margin-bottom: 15px
    border: 1px solid teal
</style>