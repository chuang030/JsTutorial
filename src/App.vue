<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from './components/HelloWorld.vue'
import Header from './components/Header.vue'
import StepBox from './components/StepBox.vue'
import ChapterBox from './components/ChapterBox.vue'
import stepJSONData from './assets/data/nvm_step_data.json'

</script>

<template>
  <div class="main">
    <Header titleText="Node js 開發環境建置"></Header>
    <ChapterBox chapteText="nvm安裝步驟"></ChapterBox>
    <StepBox :stepJSONData=stepJSONData.step></StepBox>
    <ChapterBox chapteText="vscode安裝步驟"></ChapterBox>
    <ChapterBox chapteText="建立專案"></ChapterBox>
    

  </div>
  
  

</template>

<style lang="scss">
.main {
  width: 100%;

}
</style>
