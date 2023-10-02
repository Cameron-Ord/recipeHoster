<template>
  <div>
    <input ref="name" placeholder="name.." type="text" /><input
      ref="prep"
      placeholder="prep.."
      type="text"
    /><input ref="cook" placeholder="cooking.." type="text" /><input
      ref="method"
      placeholder="methods.."
      type="text"
    />
    <p
      @click="
        submitInstructions(this.$refs.name, this.$refs.prep, this.$refs.cook, this.$refs.method)
      "
    >
      submit
    </p>
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
    getIdFromName(name) {
      axios({
        url: `${import.meta.env.VITE_APP_BASE_DOMAIN}/api/getRecipeId`,
        method: 'GET',
        params: {
          name: name.value.toLowerCase()
        }
      })
        .then((response) => {
          this.response = response['data'][0]['id']
        })
        .catch((error) => {
          error
          return error
        })
      return this.response
    },
    submitInstructions(name, prep, cook, method) {
      const Id = this.getIdFromName(name)
      console.log(Id, name.value, cook.value, method.value)
      axios({
        url: `${import.meta.env.VITE_APP_BASE_DOMAIN}/api/createInstructions`,
        method: 'POST',
        data: {
          recipeId: Id,
          recipeprep: prep.value,
          cooking: cook.value,
          methods: method.value
        }
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
