<script setup lang="ts">
import { ref, reactive } from 'vue';

type stepJSONDataType = { id: number, directions: string, imagesUrl: string }[];
const props = defineProps<{ stepJSONData: stepJSONDataType }>();

/**
 * 步驟圖物件
 */
const imagesListObject = reactive({
    listLength: props.stepJSONData.length,
    divideLength: {
        two: props.stepJSONData.length % 2,
        three: props.stepJSONData.length % 3
    },
    removedBorderBottomCount: 0
})
/**
 * 是否點開大圖
 */
const isOpenBigImage = ref(false);
/**
 * 大圖物件
 */
const bigImageObject = reactive({
    url: ""
});


const openBigImage = (imageUrl: string): void => {
    isOpenBigImage.value = true;
    bigImageObject.url = imageUrl;
}

const closeBigImage = (): void => {
    isOpenBigImage.value = false;
    bigImageObject.url = "";
}

const removedBorderBottom = (): void => {
    let windowInnerWidth: number = window.innerWidth;
    // 每行3個
    if (windowInnerWidth >= 1250) {
        if (imagesListObject.divideLength.three === 0) {
            imagesListObject.removedBorderBottomCount = 3;
            return
        }
        imagesListObject.removedBorderBottomCount = imagesListObject.divideLength.three;
        return
    }
    // 每行2個
    if (windowInnerWidth < 1250 && windowInnerWidth > 837) {
        if (imagesListObject.divideLength.two === 0) {
            imagesListObject.removedBorderBottomCount = 2;
            return
        }
        imagesListObject.removedBorderBottomCount = imagesListObject.divideLength.two;
        return
    }
    if (windowInnerWidth <= 837) {
        imagesListObject.removedBorderBottomCount = 1;
    }
}
window.addEventListener('resize', removedBorderBottom);
window.addEventListener('load', removedBorderBottom)

</script>

<template>
    <div class="step-wrapper">
        <div class="step-box" v-for="(item, index) in props.stepJSONData" :key="index"
            :class="{ 'removed-border-bottom': index >= (imagesListObject.listLength - imagesListObject.removedBorderBottomCount) }">
            <div class="step-box-directions">
                <h3>步驟{{ (index + 1) }}.</h3>
                <div class="directionsText" v-html="item.directions"></div>
            </div>
            <div class="step-box-images" :style="{ backgroundImage: 'url(' + item.imagesUrl + ')' }"  @click="openBigImage(item.imagesUrl)"></div>
        </div>
    </div>
    <div class="big-image-box" v-show="isOpenBigImage">
        <div class="big-image-box-top-button">
            <button class="button-style">
                <a :href=bigImageObject.url>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" class="bi bi-download"
                        viewBox="0 0 16 16">
                        <path
                            d="M.5 9.9a.5.5 0 0 1 .5.5v2.5a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1v-2.5a.5.5 0 0 1 1 0v2.5a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2v-2.5a.5.5 0 0 1 .5-.5z" />
                        <path
                            d="M7.646 11.854a.5.5 0 0 0 .708 0l3-3a.5.5 0 0 0-.708-.708L8.5 10.293V1.5a.5.5 0 0 0-1 0v8.793L5.354 8.146a.5.5 0 1 0-.708.708l3 3z" />
                    </svg>
                </a>
            </button>
            <button class="button-style" @click="closeBigImage()">
                <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" class="bi bi-x-circle" viewBox="0 0 16 16">
                    <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z" />
                    <path
                        d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z" />
                </svg>
            </button>
        </div>
        <div class="big-image" :style="{ backgroundImage: 'url(' + bigImageObject.url + ')' }" @click="closeBigImage()">
        </div>
    </div>
</template>

<style lang="scss">
.step-wrapper {
    padding: 1.5%;
    display: flex;
    justify-content: start;
    flex-wrap: wrap;
    position: relative;

    /* ---------------步驟區塊開始--------------- */
    .step-box {
        padding: 1%;
        width: calc(100% / 3);
        height: 450px;
        min-width: 400px;
        display: flex;
        flex-wrap: wrap;
        align-items: stretch;
        border-bottom: 3px solid rgba($color: #FFFFFF, $alpha: 0.75);
        border-right: 3px solid rgba($color: #FFFFFF, $alpha: 0.75);

        // 控制移除下border，改由js控制
        // @mixin displayBorderBottom ($start, $end) {
        //     @for $i from $start through $end {
        //         &:nth-last-of-type(#{$i}) {
        //             border-bottom: none;
        //         }
        //     }
        // }

        @media screen and (min-width: 1250px) {
            // 由js控制
            // @include displayBorderBottom(1, 3);

            &:nth-of-type(3n) {
                border-right: none;
            }
        }

        @media screen and (max-width: 1250px) {
            // 由js控制
            // @include displayBorderBottom(1, 2);
            width: calc(100% / 2);

            &:nth-of-type(2n) {
                border-right: none;
            }
        }

        @media screen and (max-width: 837px) {
            // 由js控制
            // @include displayBorderBottom(1, 1);
            width: 100%;

            &:nth-of-type(1n) {
                border-right: none;
            }
        }

        @media screen and (max-width: 600px) {
            height: 400px;
        }

        @media screen and (max-width: 475px) {
            height: 360px;
        }

        /* ---------------文字說明開始--------------- */
        .step-box-directions {
            margin-bottom: 2%;
            width: 100%;
            height: 15%;

            h3 {
                padding-bottom: 2%;
            }

            code {
                padding: 2px 4px;
                color: #c7254e;
                background-color: #f9f2f4;
                border-radius: 4px;
            }
        }

        /* ---------------文字說明結束--------------- */

        /* ---------------圖片區塊開始--------------- */
        .step-box-images {
            width: 100%;
            min-height: 70%;
            background-position: center;
            background-repeat: no-repeat;
            background-size: contain;
            cursor: pointer;

            // @media screen and (max-width:405px) {
            //     min-height: 15%;
            // }
        }

        /* ---------------圖片區塊結束--------------- */
    }

    .removed-border-bottom {
        border-bottom: none;
    }

    /* ---------------步驟區塊結束--------------- */


}

/* ---------------大圖區塊開始--------------- */
.big-image-box {
    padding: 2.5%;
    width: 90%;
    height: 90vh;
    display: flex;
    flex-wrap: wrap;
    align-items: stretch;
    position: fixed;
    top: 5%;
    left: 5%;
    background-color: rgba($color: #ffffff, $alpha: 0.9);
    border-radius: 1%;

    @media screen and (max-width:837px) {
        display: none;
    }

    .big-image-box-top-button {
        width: 100%;
        height: 10%;
        display: flex;
        justify-content: flex-end;
    }

    .big-image {
        width: 100%;
        height: 90%;
        background-position: center;
        background-repeat: no-repeat;
        background-size: contain;
    }
}

/* ---------------大圖區塊結束--------------- */


button[class=button-style] {
    padding: 0 1% 0 1%;
    border: none;
    background-color: transparent;
    color: deepskyblue;
    cursor: pointer;

    svg {
        width: 32px;
        height: 32px;

        @media screen and (max-width: 1250px) {
            width: 20px;
            height: 20px;
        }
    }
}

a[class=directions-style] {
    color: dodgerblue;
}
</style>