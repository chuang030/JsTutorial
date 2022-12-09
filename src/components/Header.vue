<script setup lang="ts">
defineProps<{ titleText: string }>()

</script>

<template>
    <div class="title">
        <div class="title-box">
            <h1>{{ titleText }}</h1>
        </div>
    </div>
</template>

<style lang="scss">
.title {
    width: 100%;
    min-width: 365px;
    margin-bottom: 3%;
    display: flex;
    justify-content: center;

    .title-box {
        width: calc(100% / 3);
        padding: 0.5%;
        border-bottom: solid white;

        h1 {
            width: 100%;
        }

        @media screen and (max-width: 1024px) {
            width: calc(100% / 2);
        }

        @media screen and (max-width: 720px) {
            width: 95%;
        }

        h1 {
            text-align: center;
            color: deepskyblue;
        }

    }
}
</style>