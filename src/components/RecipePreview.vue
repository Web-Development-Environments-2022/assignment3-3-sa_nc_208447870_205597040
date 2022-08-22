<template>
  <router-link
    :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
    class="recipe-preview"
    @click.native="addToWatched"
  >
  
   <b-card
    :title="recipe.title"
    :img-src="this.recipe.image"
    img-alt="Image"
    img-top
    style="max-width: 20rem;"
    :class="[this.watched ? 'watched' : 'mb-2']"
  >
    <b-card-text>
      <li>minutes: {{ recipe.readyInMinutes }}</li>
      <li>likes: {{ recipe.aggregateLikes }}</li>
      <div id="div_top_hypers">
        <ul id="ul_top_hypers">
          <li v-if="recipe.glutenFree"><img src="../assets/glutenfree.jpg" class="success-icon"/></li>
          <li v-if="recipe.vegan"> <img src="../assets/vegan.jpg" class="success-icon"/></li>
          <li v-if="recipe.vegetarian"> <img src="../assets/vegetarian.png" class="success-icon"/></li>
        </ul>
      <h5>add to Favorite</h5>
      <img src="../assets/like.png" class="success-icon" @click="addToFavorites"/>

      </div>

    </b-card-text>

  </b-card>

    <!-- <div class="column">
          <div class="card">
            <img :src="this.$root.store.iconsLinks.readyInMinutes" style="width:100%"/>
              <div class="container">
                <div :title="recipe.title" class="recipe-title">
                    {{ recipe.title }}
                </div>
                <ul class="recipe-overview">
                  <li>{{ recipe.readyInMinutes }} minutes</li>
                  <li>{{ recipe.aggregateLikes }} likes</li>
                  <li v-if="recipe.glutenFree"> gluten-Free</li>
                  <li v-if="recipe.vegan"> vegan</li>
                  <li v-if="recipe.vegetarian"> vegetarian</li>
                  <li ></li>
                </ul>
            </div>
          </div>
      </div> -->


  </router-link>
</template>

<script>
export default {
  data() {
    return {
      watched: false
    };
  },
  props: {
    recipe: {
      type: Object,
      required: true
    }

    // id: {
    //   type: Number,
    //   required: true
    // },
    // title: {
    //   type: String,
    //   required: true
    // },
    // readyInMinutes: {
    //   type: Number,
    //   required: true
    // },
    // image: {
    //   type: String,
    //   required: true
    // },
    // aggregateLikes: {
    //   type: Number,
    //   required: false,
    //   default() {
    //     return undefined;
    //   }
    // }
  },
  methods: {
     async addToWatched(){
        console.log(this.recipe.id);
        const watched = await this.axios.get(this.$root.store.server_domain + "/users/WatchedRecipes");
        console.log(watched);

        // for (let i = 0; i < watched.length; i++) {
        //   if(this.recipe.id === watched[i])
        //     return;
        // }
        // const res = await this.axios.post(this.$root.store.server_domain + "/users/WatchedRecipes", {
        //   recipe_id: this.recipe.id,
        // });
     },
     async addToFavorites(){
      const favorites = await this.axios.get(this.$root.store.server_domain + "/users/favorites");
      if(favorites.includes(this.recipe.id)){
        alert("already exist");
      }
      const response = await this.axios.post(
        this.$root.store.server_domain + "/users/favorites",
        {
            recipe_id: this.recipe.id,
        }
      );
    }
  }
};
</script>

<style scoped>
#div_top_hypers {
    background-color:#eeeeee;
    display:inline;      
}
#ul_top_hypers li{
    display: inline;
}
.success-icon {
  border-radius: 5px;
  width: 40px;
  height: 40px;
  display: inline-block;
}

.recipe-preview .recipe-footer {
  width: 100%;
  height: 80%;
  overflow: hidden;
}


.recipe-preview .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;
  text-align: center;
}



body {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0;
}

html {
  box-sizing: border-box;
}

*, *:before, *:after {
  box-sizing: inherit;
}

.column {
  float: left;
  width: 33.3%;
  margin-bottom: 16px;
  padding: 0 8px;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  margin: 8px;
  width: 500px;
}

.about-section {
  padding: 50px;
  text-align: center;
  background-color: #474e5d;
  color: white;
}


.watched {
  color: blueviolet;
}

.button {
  border: none;
  outline: 0;
  display: inline-block;
  padding: 8px;
  color: white;
  background-color: #000;
  text-align: center;
  cursor: pointer;
  width: 100%;
}

.button:hover {
  background-color: #555;
}

@media screen and (max-width: 650px) {
  .column {
    width: 100%;
    display: block;
  }
}
img {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 5px;
}

</style>
