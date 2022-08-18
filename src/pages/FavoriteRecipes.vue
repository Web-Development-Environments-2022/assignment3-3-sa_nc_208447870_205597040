<template>
    <div>
        <div v-for="(r,index) in this.recipes" :key="index">
            <RecipePreview :recipe="r"></RecipePreview>
        </div>

    </div>
</template>

<script>
import RecipePreview from '../components/RecipePreview.vue';

export default{
    name:"FavoriteRecipes",
    data(){
        return {
            recipes: null
        }
    },
    components:{
        RecipePreview
    }
}
</script>


<style>

</style>