<template>
  <b-container>
    <h3>
      {{ title }}:
      <slot></slot>
    </h3>
    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <RecipePreview title="recipe" class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
    <button @click="updateRecipes" v-if="title==='Explore'">More</button>
  </b-container>
</template>

<script>
import { title } from "process";
import RecipePreview from "./RecipePreview.vue";
export default {
  name: "RecipePreviewList",
  components: {
    RecipePreview
  },
  props: {
    title: {
      type: String,
      required: false
    }
  },
  data() {
    return {
      recipes: []
    };
  },
  mounted() {  
    if(this.props?.title==="Family Recipes"){
      this.familyRecipes()
    }
    else if(this.props?.title==="Favorites Recipes"){
      this.favorites()
    }
    else if(this.props?.title==="My Recipes"){
      this.myRecipes()
    }
    else{
      console.log(":server domain: "+this.$root.store.server_domain);
      this.updateRecipes();
    }
    
  },
  methods: {
    async updateRecipes() {
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/recipes/random",
          // "https://test-for-3-2.herokuapp.com/recipes/random"
          
        );

        // console.log(response);
        const recipes = response.data.recipes;
        this.recipes = [];
        this.recipes.push(...recipes);
        // console.log(this.recipes);
      } catch (error) {
        console.log(error);
      }
    },
    async favorites(){
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/users/favorites",
        );
        // console.log(response.data);
        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
      } catch (error) {
        console.log(error);
      }
    },
    async myRecipes(){
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/users/myRecipes",
        );
        console.log(response.data);
        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
      } catch (error) {
        console.log(error);
      }
    },
    async familyRecipes(){
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/users/familyRecipes",
        );
        console.log(response.data);
        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
      } catch (error) {
        console.log(error);
      }
    },
  }
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 400px;
}
</style>
