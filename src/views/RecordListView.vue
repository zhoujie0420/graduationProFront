<template>
  <section>
    <van-nav-bar title="问诊记录"
                 fixed
                 placeholder
                 safe-area-inset-top
                 left-arrow
                 @click-left="onClickLeft"

    />
  </section>

  <van-cell-group>
    <van-cell v-for="(item, index) in cellItems" :key="index" :title="item.consultationDate" :label="item.patientName" :is-link="item.isLink" center />

  </van-cell-group>

  <van-divider/>

</template>

<script setup>
// import usePeerStore from "@/store/peer";
import router from "@/router";
import {reactive} from "vue";
import $ from "jquery";
import {apiUrl} from "../../config";
import usePeerStore from "@/store/peer";
const peerStore = usePeerStore();
let cellItems = reactive([]);
cellItems = [
  {
    consultationDate: "2021-06-01",
    patientName: "患者：张三",
    isLink: true,
  },
  ]

const getCellItems = () =>{
  $.ajax({
    url: `${apiUrl}/api/record/list/`,
    type: "post",
    data: {
      id: peerStore.username,
    },
    headers: {
      Authorization: "Bearer " + peerStore.token,
    },
    success(resp) {
      cellItems.push(...resp.data);
    }
  })
}
getCellItems();
console.log(cellItems)


const onClickLeft = () => {
  router.push("/setting-view");
}


</script>

<style scoped lang="scss">
.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* 可根据需要调整容器高度 */
}

.wide-button {
  width: 200px; /* 根据需要调整按钮宽度 */
  margin-top: -50px; /* 根据需要调整按钮上边距 */
}

</style>