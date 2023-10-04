<template>
  <main class="pageMain">
    <section class="LoginSection">
      <admin-login></admin-login>
    </section>
    <section class="RecipeUploadSection">
      <recipe-uploader></recipe-uploader>
    </section>
    <section class="InstructionsUploadSection">
      <instructions-uploader></instructions-uploader>
    </section>
    <section class="NutritionalDataUpload">
      <nutrition-data></nutrition-data>
    </section>
  </main>
</template>

<script>
import NutritionData from '../components/NutritionData.vue'
import AdminLogin from '../components/AdminLogin.vue';
import InstructionsUploader from '../components/InstructionsUploader.vue'
import RecipeUploader from '../components/RecipeUploader.vue'
export default {
  components: {
    RecipeUploader,
    InstructionsUploader,
    AdminLogin,
    NutritionData
  }
}
</script>

<style lang="scss" scoped>
.pageMain{
  min-height: 100vh;
  display: grid;
  align-items: center;
  grid-template-columns:1fr 1fr 1fr 1fr;
  
  >.NutritionalDataUpload{
    display: grid;
  }
  >.InstructionsUploadSection{
    display: grid;
  }
  >.RecipeUploadSection{
    display: grid;
  }
  >.LoginSection{
    display: grid;
  }
}
</style>
