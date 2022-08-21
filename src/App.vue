<template>

  <div id="app">
    
    <div id="nav">
      <router-link :to="{ name: 'main' }" class="btn btn-outline-success my-2 my-sm-0">Vue Recipes</router-link>
      <router-link :to="{ name: 'search' }" class="btn btn-outline-success my-2 my-sm-0">Search</router-link>
      <router-link :to="{ name: 'about' }" class="btn btn-outline-success my-2 my-sm-0">About</router-link>

      <!-- use the modal component, pass in the prop -->

      <modal :show="showModal" @close="showModal = false"></modal>


      <span id="side_btn" class="btn btn-outline-success my-2 my-sm-0" v-if="!$root.store.username">
        Guest:
        <router-link :to="{ name: 'register' }">Register</router-link>|
        <router-link :to="{ name: 'login' }">Login</router-link>|
      </span>
      <span v-else>
        {{ $root.store.username }}: <button class="btn btn-outline-success my-2 my-sm-0" @click="Logout">Logout</button>|
        <button @click="CreateRecipe">Add recipe</button>|
        <b-dropdown variant="success" id="dropdown-1" :text="$root.store.username">
          <b-dropdown-item><router-link :to="{ name: 'FamilyRecipes' }">Family recipes</router-link></b-dropdown-item>
          <b-dropdown-item><router-link :to="{ name: 'FavoriteRecipes' }">Favorite recipes</router-link></b-dropdown-item>
          <b-dropdown-item><router-link :to="{ name: 'MyRecipes' }">My recipes</router-link></b-dropdown-item>
        <b-dropdown-divider></b-dropdown-divider>
      </b-dropdown>

      </span>
    </div>

    <v-container class="grey lighten-5 mb-6">
      <v-row
        no-gutters
        style="height: 150px;"
      >
        <v-col>
        <router-view />
            <RecipePreviewList title="Explore"></RecipePreviewList>

        </v-col>
      </v-row>
    </v-container>
    

      
  </div>
</template>

<script>
import RecipePreviewList from './components/RecipePreviewList.vue';
import Modal from './components/Modal.vue';

export default {
  name: "App",
  data() {
    return {
      showModal: false
    }
  },
  components: {
    RecipePreviewList,
    Modal,
},
  methods: {
    Logout() {
      this.$root.store.logout();
      this.$root.toast("Logout", "User logged out successfully", "success");

      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    },
    CreateRecipe() {
      
    }
  }
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#side_btn {
    color: rgb(3, 2, 2);
    font-size: 18px;
    padding: 3px 15px;
    margin-top: 4px;
    margin-right: 10px;
    display: block;
    float: right;
    border-radius: 5px;
}

</style>
