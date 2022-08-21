<template>
    <div>
        <RecipePreviewList title="Family Recipes"></RecipePreviewList>
    </div>
</template>

<script>
import RecipePreviewList from '../components/RecipePreviewList.vue';

export default{
    name:"FamilyRecipes",
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