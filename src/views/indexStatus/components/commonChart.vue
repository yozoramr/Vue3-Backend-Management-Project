<script setup>
import '@/styles/standardStyle.css'
import { onMounted, ref } from 'vue'

const props = defineProps({
  chartStatus: Object
})
const percent = (props.chartStatus.numberMin / props.chartStatus.numberMax) * 100
const mainBoxRef = ref(null)
onMounted(() => {
  if(mainBoxRef.value){
      mainBoxRef.value.addEventListener('mouseenter', () => {
      mainBoxRef.value.classList.add('mainBoxFocus')
    })
    mainBoxRef.value.addEventListener('mouseleave', () => {
      mainBoxRef.value.classList.remove('mainBoxFocus')
    })
  }
})


</script>
<template>
  <div class="body--chart commonShadows" ref="mainBoxRef">
    <div class="block--chart">
      <div class="item--title">
        <span>{{ chartStatus.tittle }}</span>
      </div>
      <div class="item__block">
        <div class="chartNum">{{ chartStatus.numberMin + "/" + chartStatus.numberMax}}</div>
        <div class="chartBar">
          <div class="insideBar" :style="{ width: percent + '%' }"></div>
        </div>
      </div>
      <div class="item--subheading">{{ chartStatus.subheading }}</div>
    </div>
  </div>
</template>
<style scoped lang="less">
.mainBoxFocus{
  box-shadow: 1px 1px 8px rgba(0, 0, 0, 0.2);
}
.body--chart {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  .block--chart {
    height: 140px;
    width: 100%;
    padding: 0 18px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    .item--title {
      height: 26px;
      font-size: 26px;
    }
    .item__block {
      .chartNum {
        color: #cccccc;
        font-size: 12px;
        margin-bottom: 3px;
      }
      .chartBar {
        width: 100%;
        height: 3px;
        background-color: #ccc;
        .insideBar {
          width: 0;
          height: 3px;
          background-color: #3fb1e3;
        }
      }
    }
    .item--subheading {
      font-size: 10px;
      color: #cccccc;
    }
  }
}
</style>