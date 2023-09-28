<template>
  <main>
    <section>
      <recipe-uploader></recipe-uploader>
    </section>
    <section>
      <instructions-uploader></instructions-uploader>
    </section>
  </main>
</template>

<script>
import InstructionsUploader from '../components/InstructionsUploader.vue'
import RecipeUploader from '../components/RecipeUploader.vue'
export default {
  components: {
    RecipeUploader,
    InstructionsUploader,
    
  }
}
</script>

<style lang="scss" scoped></style>
