<script setup lang="ts">
const props = defineProps<{ chapteText: string, isClick: boolean }>()
</script>

<template>
    <div class="chapter-wrapper">
        <h2 :class="{ active: props.isClick }">
            {{ chapteText }}
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-caret-down"
                viewBox="0 0 16 16" :class="{ active: props.isClick }">
                <path
                    d="M3.204 5h9.592L8 10.481 3.204 5zm-.753.659 4.796 5.48a1 1 0 0 0 1.506 0l4.796-5.48c.566-.647.106-1.659-.753-1.659H3.204a1 1 0 0 0-.753 1.659z" />
            </svg>
        </h2>
    </div>
</template>

<style lang="scss">
.chapter-wrapper {
    margin-top: 1%;
    margin-bottom: 1%;
    width: 100%;
    min-width: 395px;
    text-align: center;
    cursor: pointer;
}

h2[class=active] {
    color: deepskyblue;
    transition: all ease 200ms;
}

h2 {
    color: black;
    transition: all ease 300ms;
}

svg[class="bi bi-caret-down active"] {
    color: deepskyblue;
    transform: rotate(180deg);
    transition: all ease 300ms;
}

svg[class="bi bi-caret-down"] {
    color: black;
    transition: all ease 300ms;
}
</style>