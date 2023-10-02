<template>
  <main>
    <section>
      <admin-login></admin-login>
    </section>
    <section>
      <recipe-uploader></recipe-uploader>
    </section>
    <section>
      <instructions-uploader></instructions-uploader>
    </section>
  </main>
</template>

<script>
import AdminLogin from '../components/AdminLogin.vue';
import InstructionsUploader from '../components/InstructionsUploader.vue'
import RecipeUploader from '../components/RecipeUploader.vue'
export default {
  components: {
    RecipeUploader,
    InstructionsUploader,
    AdminLogin
  }
}
</script>

<style lang="scss" scoped></style>
