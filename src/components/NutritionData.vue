
<template>
    <span class="nutritionInputs">
        <h3>Nutrition</h3>
        <div class="inputDiv">
            <input placeholder="name" type="text" ref="name">
            <input placeholder="protein" type="text" ref="protein">
            <input placeholder="fat" type="text" ref="fat">
            <input placeholder="carbs" type="text" ref="carbs">
            <input placeholder="calories" type="text" ref="calories">
            <input placeholder="saturatedfat" type="text" ref="saturatedFat">
            <input placeholder="sugar" type="text" ref="sugar">
            <input placeholder="salt" type="text" ref="salt">
        </div>
        <p @click="submitNutrition" class="submitTag">Submit</p>
    </span>
</template>

<script>
import Cookies from 'vue-cookies';
import axios from 'axios';
    export default {
        components:{

        },

        data() {
            return {

            }
        },

        methods:{

            getIdFromName(name){
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

            submitNutrition(){
                const adminCreds = Cookies.get('adminInfo');
                const id = this.getIdFromName(this.$refs.name)
                const proteinValue = parseFloat(this.$refs.protein.value);
                const fatValue = parseFloat(this.$refs.fat.value);
                const carbValue = parseFloat(this.$refs.carbs.value);
                const calValue = parseFloat(this.$refs.calories.value);
                const satFatValue = parseFloat(this.$refs.saturatedFat.value);
                const sugarValue = parseFloat(this.$refs.sugar.value);
                const saltValue = parseInt(this.$refs.salt.value);
                axios({
                    url: `${import.meta.env.VITE_APP_BASE_DOMAIN}/api/createNutritionalProfile`,
                    method: 'POST',
                    data:{
                        recipe_id: id,
                        protein: proteinValue,
                        fat: fatValue,
                        carbs: carbValue,
                        calories: calValue,
                        saturatedfat: satFatValue,
                        sugars: sugarValue,
                        salt: saltValue,
                        token: adminCreds['session_token'],
                        admin_id: adminCreds['admin_id'],
                    }
                }).then((response)=>{
                    response;
                }).catch((error)=>{
                    error
                })
            }
        },
        computed:{

        },
        created(){

        },
        mounted(){

        },
        beforeMount(){

        },
        beforeUpdate(){

        },
        updated(){

        },
        beforeUnmount(){

        },
        unmounted(){

        }

    }
</script>

<style lang="scss" scoped>
.nutritionInputs{
    display: grid;
    align-items: center;
    justify-items: center;
    grid-auto-flow: row;
    row-gap: 25px;
    >.inputDiv{
        display: grid;
        justify-items: center;
        grid-auto-flow: row;
        row-gap: 10px;
        >input{
            padding: 10px;
        }
    }

    >p{
        padding: 5px;
    }
}
</style>


