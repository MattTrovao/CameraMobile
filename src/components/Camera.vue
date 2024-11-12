<script setup>
import { onMounted, ref } from "vue";

const previewUrl = ref(null);

function showPreview(event) {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      previewUrl.value = e.target.result;
      console.log("preview", previewUrl.value);
    };
    reader.readAsDataURL(file);
  }
}

  const userLocationPermission = ref(false);
const userLocation = ref("");

const successCallback = (position) => {
  userLocationPermission.value = true;
  userLocation.value = position;
};

const errorCallback = () => {
  toast.error(t("webExecution.locationPermissionDenied"));
};

const getLocation = () => {
  navigator.geolocation.getCurrentPosition(successCallback, errorCallback);
};

onMounted(() => {
  getLocation();
});
</script>

<template>
  <div class="item">
    <label for="" class="bold font-default">Camera</label>
    <input
      type="file"
      accept="image/*"
      capture="camera"
      @change="showPreview"
    />

    <img id="preview" :src="previewUrl" alt="Preview" v-if="previewUrl" />

    <hr/>
    
    <button @click="getLocation">
      Permitir Acesso a Localização
    </button>
  </div>
</template>

<style lang="scss" scoped>
#preview {
  object-fit: contain;
  width: 400px;
  height: 400px;
}
</style>
