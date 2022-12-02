<script setup lang="ts">
defineProps<{ chapteText: string }>()
</script>

<template>
    <div class="chapter-wrapper">
        <h2>{{ chapteText }}</h2>
    </div>
</template>

<style lang="scss">
    .chapter-wrapper {
        margin-top: 1%;
        margin-bottom: 1%;
        width: 100%;
        text-align: center;
    }
</style>