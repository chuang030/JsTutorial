<script setup lang="ts">
type stepJSONDataType = { id: number, directions: string, imagesUrl: string }[];
const props = defineProps<{ stepJSONData: stepJSONDataType }>();
</script>

<template>
    <div class="step-wrapper">
        <div class="step-box" v-for="(item, index) in props.stepJSONData" :key="index">
            <div class="step-box-directions">
                <h3>步驟{{ (index + 1) }}.</h3>
                <div class="directionsText" v-html="item.directions"></div>
            </div>
            <div class="step-box-images" :style="{ backgroundImage: 'url(' + item.imagesUrl + ')' }">
                <!-- <img :src=item.imagesUrl alt=""> -->
            </div>
        </div>
    </div>
</template>

<style lang="scss">
.step-wrapper {
    padding: 1.5%;
    display: flex;
    justify-content: start;
    flex-wrap: wrap;

    .step-box {
        padding: 1%;
        width: calc(100% / 3);
        height: 400px;
        min-width: 400px;
        border-bottom: 2px solid rgba($color: #FFFFFF, $alpha: 0.75);
        border-right: 2px solid rgba($color: #FFFFFF, $alpha: 0.75);

        &:nth-of-type(3n) {
            border-right: none;
        }

        @media screen and (max-width: 1200px) {
            width: calc(100% / 2);

            &:nth-of-type(2n) {
                border-right: none;
            }
        }
        
        @media screen and (max-width: 800px) {
            width: 100%;

            &:nth-of-type(1n) {
                border-right: none;
            }
        }

        .step-box-directions {
            margin-bottom: 2%;
            width: 100%;
        }

        .step-box-images {
            // display: flex;
            // justify-content: center;
            width: 100%;
            // width: 250px;
            // height: fill-available;
            height: 250px;
            background-position: center;
            background-repeat: no-repeat;
            background-size: contain;
            // overflow: hidden;
            cursor: pointer;

            img {
                width: auto;
                height: auto;
            }
        }
    }



}

a {
    color: dodgerblue;
}
</style>