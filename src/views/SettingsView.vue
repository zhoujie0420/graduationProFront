<template>
  <section>
    <van-nav-bar title="设置"
                 fixed
                 placeholder
                 safe-area-inset-top/>
  </section>

  <section>
    <van-cell-group :title="getTitle()" inset>
      <van-cell title="用户名" :value=" peerStore.username "/>
      <van-cell title="手机号" :value=" peerStore.phone" clickable/>
      <van-cell title="身份" :value="getRole()" clickable/>
    </van-cell-group>
  </section>

  <van-divider/>
  <div class="center-container">
    <van-button class="wide-button" type="danger" @click="logout">退出</van-button>
  </div>

</template>

<script setup>
import usePeerStore from "@/store/peer";
import router from "@/router";


const getTitle = () => {
  if (peerStore.role == 1) {
    return "祝您早日康复";
  } else if (peerStore.role == 2) {
    return "悬壶济世，妙手回春";
  }
};

const getRole = () =>{
  if (peerStore.role == 1) {
    return "患者";
  } else if (peerStore.role == 2) {
    return "医生";
  }
}


const logout = () => {
  localStorage.removeItem("jwt_token");
  peerStore.id = "";
  peerStore.username = "";
  peerStore.email = "";
  peerStore.photo = "";
  peerStore.token = "";
  peerStore.is_login = false;

  router.push("/login-view");

}


const peerStore = usePeerStore();
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