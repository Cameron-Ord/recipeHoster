<template>
  <div>
    <input placeholder="name" class="title" ref="title" type="text" />
    <input placeholder="desc" class="desc" ref="desc" type="text" />
    <input placeholder="ingredients" class="ingredient" ref="ingredients" type="text" />
    <input placeholder="cuisine" class="cuisine" ref="cuisine" type="text" />
    <input class="isHealthy" ref="isHealthy" type="checkbox" />
    <input class="image" ref="image" type="file" />
    <p @click="sendRecipe">Submit</p>
  </div>
</template>

<script>
import Cookies from 'vue-cookies';
import axios from 'axios'
export default {
  components: {},

  data() {
    return {}
  },

  methods: {
    createForm() {
      const admin_ = Cookies.get('adminInfo');
      let form = new FormData()
      const isHealthy = this.checkIfHealthy()
      if (this.$refs.image.files[0] !== undefined) {
        form.append('title', this.$refs.title.value.toLowerCase())
        form.append('desc', this.$refs.desc.value.toLowerCase())
        form.append('image', this.$refs.image.files[0])
        form.append(
          'image_url',
          `${import.meta.env.VITE_APP_BASE_DOMAIN}/images/`
        )
        form.append('ingredients', this.$refs.ingredients.value.toLowerCase())
        form.append('isHealthy', isHealthy)
        form.append('cuisine', this.$refs.cuisine.value.toLowerCase())
        form.append('token', admin_['session_token']);
        form.append('admin_id', admin_['admin_id']);
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
      console.log(form)
      axios({
        url: `${import.meta.env.VITE_APP_BASE_DOMAIN}/api/postRecipe`,
        method: 'POST',
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
