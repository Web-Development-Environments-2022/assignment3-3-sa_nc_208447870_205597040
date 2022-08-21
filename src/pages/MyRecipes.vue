<template>
    <div>
        <RecipePreviewList title="My Recipes"></RecipePreviewList>
    </div>
</template>

<script>
import RecipePreviewList from '../components/RecipePreviewList.vue';

export default{
    name:"MyRecipes",
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