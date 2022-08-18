<template>

  <div id="app">
    
    <!-- <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li >
            <router-link :to="{ name: 'main' }" class="nav-link">Vue Recipes <span class="sr-only">(current)</span></router-link>
          </li>
          <li class="nav-item">
            <router-link :to="{ name: 'search' }" class="nav-link">Search <span class="sr-only">(current)</span></router-link>
          </li>
          <li class="nav-item">
            <router-link :to="{ name: 'about' }" class="nav-link">About <span class="sr-only">(current)</span></router-link>
          </li>

          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              Dropdown
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a class="dropdown-item" href="#">Action</a>
              <a class="dropdown-item" href="#">Another action</a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#">Something else here</a>
            </div>
          </li>

          <li class="nav-item">
            <a><modal :show="showModal" class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</modal></a>
            <modal :show="showModal" @close="showModal = false">
              <h3>custom header</h3>
            </modal> 
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
        
        
      </div>
    </nav> -->
    <div id="nav">
      <router-link :to="{ name: 'main' }" class="btn btn-outline-success my-2 my-sm-0">Vue Recipes</router-link>
      <router-link :to="{ name: 'search' }" class="btn btn-outline-success my-2 my-sm-0">Search</router-link>
      <router-link :to="{ name: 'about' }" class="btn btn-outline-success my-2 my-sm-0">About</router-link>

      <!-- use the modal component, pass in the prop -->
      <button class="btn btn-outline-success my-2 my-sm-0" id="show-modal" @click="showModal = true">Show Modal</button>

      <modal :show="showModal" @close="showModal = false">
          <h3>custom header</h3>
      </modal>

      <b-dropdown variant="success" id="dropdown-1" :text="$root.store.username">
        
        <b-dropdown-item><router-link :to="{ name: 'FamilyRecipes' }">Family recipes</router-link></b-dropdown-item>
        <b-dropdown-item><router-link :to="{ name: 'FavoriteRecipes' }">Favorite recipes</router-link></b-dropdown-item>
        <b-dropdown-item><router-link :to="{ name: 'MyRecipes' }">My recipes</router-link></b-dropdown-item>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item active>Active action</b-dropdown-item>
        <b-dropdown-item disabled>Disabled action</b-dropdown-item>
      </b-dropdown>



      <span id="side_btn" class="btn btn-outline-success my-2 my-sm-0" v-if="!$root.store.username">
        Guest:
        <router-link :to="{ name: 'register' }">Register</router-link>|
        <router-link :to="{ name: 'login' }">Login</router-link>|
      </span>
      <span v-else>
        {{ $root.store.username }}: <button @click="Logout">Logout</button>|
        <button @click="CreateRecipe">Add recipe</button>|
      </span>
    </div>
    <router-view />
    <RecipePreviewListVue></RecipePreviewListVue>
  </div>
</template>

<script>
import RecipePreviewListVue from './components/RecipePreviewList.vue';
import Modal from './components/Modal.vue';

export default {
  name: "App",
  data() {
    return {
      showModal: false
    }
  },
  components: {
    RecipePreviewListVue,
    Modal,
    Modal
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
