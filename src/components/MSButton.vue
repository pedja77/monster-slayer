<template>
  <button :id="id" @click="emitButtonType">{{ caption }}</button>
</template>

<script>
export default {
    props: ['id', 'caption', 'action'],
    methods: {
        emitButtonType() {
            //console.log(this.action)
            this.$emit(this.action)
        }
    }
}
</script>


