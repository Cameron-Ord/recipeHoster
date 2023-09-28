<template>
  <div>
    <input class="title" ref="title" type="text" />
    <input class="desc" ref="desc" type="text" />
    <input class="ingredient" ref="ingredients" type="text" />
    <input class="cuisine" ref="cuisine" type="text" />
    <input class="isHealthy" ref="isHealthy" type="checkbox" />
    <input class="image" ref="image" type="file" />
    <p @click="sendRecipe">Submit</p>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  components: {},

  data() {
    return {}
  },

  methods: {
    createForm() {
      let form = new FormData()
      const isHealthy = this.checkIfHealthy()
      if (this.$refs.image.files[0] !== undefined) {
        form.append('title', this.$refs.title.value)
        form.append('desc', this.$refs.desc.value)
        form.append('image', this.$refs.image.files[0])
        form.append(
          'image_url',
          `${import.meta.env.VITE_APP_BASE_DOMAIN}/images/${this.$refs.image.files[0]['name']}`
        )
        form.append('ingredients', this.$refs.ingredients.value)
        form.append('isHealthy', isHealthy)
        form.append('cuisine', this.$refs.cuisine.value)
      } else {
        console.log('an image is required')
      }
      return form
    },

    checkIfHealthy() {
      let isHealthy = 0
      const isChecked = this.$refs.isHealthy.checked
      if (isChecked) {
        isHealthy = 1
      } else {
        isHealthy = 0
      }

      return isHealthy
    },

    sendRecipe() {
      const form = this.createForm()
      axios({
        url: `${import.meta.env.VITE_APP_BASE_DOMAIN}/api/postRecipe`,
        method: 'POST',
        headers: {
          'Content-Type': 'multipart/form-data'
        },
        data: form
      })
        .then((response) => {
          response
        })
        .catch((error) => {
          error
        })
    }
  },
  computed: {},
  created() {},
  mounted() {},
  beforeMount() {},
  beforeUpdate() {},
  updated() {},
  beforeUnmount() {},
  unmounted() {}
}
</script>

<style lang="scss" scoped></style>
