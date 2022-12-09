<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import Header from './components/Header.vue'
import StepBox from './components/StepBox.vue'
import ChapterBox from './components/ChapterBox.vue'
import nvmStepJSONData from './assets/data/nvm_step_data.json'
import vscodeStepJSONData from './assets/data/vscode_step_data.json'
import createProjectStepJSONData from './assets/data/create_project_step_data.json'
import { ref } from 'vue'

const pageList: string[] = ["nvmStep", "vscodeStep", "createProject"];
const clickItem = ref("nvmStep");
const showItem = (boxId: string): void => {
  if (clickItem.value === boxId) {
    clickItem.value = "";
    return
  }
  clickItem.value = boxId;
}

</script>

<template>
  <main class="main">
    <Header titleText="Node js 開發環境建置"></Header>
    <ChapterBox chapteText="nvm安裝步驟" @click="showItem('nvmStep')" :isClick="clickItem === pageList[0]"></ChapterBox>
    <div class="nvm-step" v-show="clickItem === pageList[0]">
      <StepBox :stepJSONData=nvmStepJSONData.step></StepBox>
    </div>
    <ChapterBox chapteText="vscode安裝步驟" @click="showItem('vscodeStep')" :isClick="clickItem === pageList[1]">
    </ChapterBox>
    <div class="vscode-step" v-show="clickItem === pageList[1]">
      <StepBox :stepJSONData=vscodeStepJSONData.step></StepBox>
    </div>
    <ChapterBox chapteText="建立專案" @click="showItem('createProject')" :isClick="clickItem === pageList[2]"></ChapterBox>
    <div class="create-project" v-show="clickItem === pageList[2]">
      <StepBox :stepJSONData=createProjectStepJSONData.step></StepBox>
    </div>
  </main>



</template>

<style lang="scss">
main {
  width: 100%;
}
</style>
