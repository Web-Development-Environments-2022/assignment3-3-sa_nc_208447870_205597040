<template>
    <div>
        <RecipePreviewList title="Favorites Recipes"></RecipePreviewList>
    </div>
</template>

<script>
import RecipePreviewList from '../components/RecipePreviewList.vue';

export default{
    name:"FavoriteRecipes",
    data(){
        return {
            recipes: null
        }
    },
    components:{
        RecipePreviewList
    }
}
</script>


<style>

</style>