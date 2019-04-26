<template>
    <button @click='checkFlag'>
        check
    </button>
</template>

<script>
export default {
    name: 'check-flag',
    methods: {
        checkFlag(){
            this.$emit('checkFlag');
        }
    }
}
</script>

<style>

</style>
