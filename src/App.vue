<script setup>
import { onMounted, ref } from "vue";
import Camera from "./components/Camera.vue";

const showCamera = ref(false);

function getMobileOperatingSystem() {
  var userAgent = navigator.userAgent || navigator.vendor || window.opera;
  if (
    /windows phone/i.test(userAgent) ||
    /android/i.test(userAgent) ||
    (/iPad|iPhone|iPod/.test(userAgent) && !window.MSStream)
  ) {
    showCamera.value = true;
  }
}

onMounted(() => {
  getMobileOperatingSystem();
});
</script>

<template>
  <main class="container">
    <div class="row">
      <Camera v-if="showCamera"/>

      <div class="text-center" v-else>
        <h1 class="bold">
          ERRO!!!
        </h1>
        <p>
          A aplicação funciona apenas em dispositivos: <b>Android, iOS, Windows Phone</b>
        </p>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
