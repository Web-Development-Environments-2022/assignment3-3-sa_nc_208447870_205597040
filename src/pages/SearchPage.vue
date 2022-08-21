<template>
  <v-container class="pa-0 mb-12 d-flex flex-column ">
    <v-row class="mt-12">
      <v-col cols="12" class=" d-flex justify-center mb-3">
        <input type="text" v-model="searchWord" class="input-field mt-0" placeholder="מה תרצו לחפש היום?">
      </v-col>
      <div class="form-group">
        <label style="width:100px;display:inline-block;" for="exampleInputEmail1">Results</label>
        <select v-model="Results_num" value="5" style="width:150px;display:inline-block;" class="form-control form-control-sm">
          <option>5 </option>
          <option>10 </option>
          <option>15</option>
        </select>
      </div>

      <div class="pageList">
        
        <label style="width:100px;display:inline-block;" for="exampleInputEmail1">Filter by Cuisines</label>
        <select v-model="Cuisines" style="width:150px;display:inline-block;" class="form-control form-control-sm">
          <option></option> 
          <option>African</option>
          <option>American</option>
          <option>British</option>
          <option>Cajun</option>
          <option>Caribbean</option>
          <option>Chinese</option>
          <option>Eastern European</option>
          <option>European</option>
          <option>French</option>
          <option>German</option>
          <option>Greek</option>
          <option>Indian</option>
          <option>Irish</option>
          <option>Italian</option>
          <option>Japanese</option>
          <option>Jewish</option> 
          <option>Korean</option> 
          <option>Latin American</option>
          <option>Mediterranean</option> 
          <option>Mexican</option> 
          <option>Middle Eastern</option> 
          <option>Nordic</option> 
          <option>Southern</option>
          <option>Spanish</option>
          <option>Thai</option>
          <option>Vietnamese</option>
        </select>
      </div>
      <div class="pageList">
        <label style="width:100px;display:inline-block;" for="exampleInputEmail1">Filter by diet</label>
        <select v-model="Diet" style="width:150px;display:inline-block;" class="form-control form-control-sm">
          <option></option> 
          <option>Gluten Free</option>
          <option>Ketogenic</option>
          <option>Vegetarian</option>
          <option>Lacto-Vegetarian</option>
          <option>Ovo-Vegetarian</option>
          <option>Vegan</option>
          <option>Pescetarian</option>
          <option>Paleo</option>
          <option>Primal</option>
          <option>Low FODMAP</option>
          <option>Whole30</option>
        </select>
      </div>

       <div class="pageList">
        <label style="width:100px;display:inline-block;" for="exampleInputEmail1">Intolerances</label>
        <select value="" v-model="Intolerances" v-bin style="width:150px;display:inline-block;" class="form-control form-control-sm">
          <option></option> 
          <option>Dairy</option> 
          <option>Egg</option> 
          <option>Gluten</option> 
          <option>Grain</option> 
          <option>Peanut</option> 
          <option>Seafood</option> 
          <option>Sesame</option>
          <option>Shellfish</option> 
          <option>Soy</option> 
          <option>Sulfite</option> 
          <option>Tree Nut</option> 
          <option>Wheat</option>
        </select>
      </div>

      <v-col cols="12" class="d-flex justify-center align-center  mb-4 mt-3 ">
        <v-btn class="btn btn-outline-success my-2 my-sm-0" @click="startSearch">Search </v-btn>
      </v-col>
      <v-col cols="12" class="d-flex justify-center align-center  mb-4 mt-3 ">
        <v-btn  :disable="onSearch" :class="[onSearch ? 'btn btn-outline-success my-2 my-sm-0' : 'gray']" @click="TimeSort">Sort by Time </v-btn>
      </v-col>
      <v-col cols="12" class="d-flex justify-center align-center  mb-4 mt-3 ">
        <v-btn :disable="onSearch" :class="[onSearch ? 'btn btn-outline-success my-2 my-sm-0' : 'gray']" @click="PopolaritySort">Sort by Popolarity </v-btn>
      </v-col>
      <v-col v-if="!loaded" class="d-flex justify-center align-center spinner mt-12 " cols="12">
        <BreedingRhombusSpinner :animation-duration="infinite" :size="70" :color="'tomato'" />
      </v-col>
      <v-col v-if="onSearch && recipes.length===0">
        <h1>No Results</h1>
      </v-col>
      <v-col v-if="onSearch && recipes.length>0">
        <b-row>
          <b-col v-for="r in recipes" :key="r.id">
            <RecipePreview title="recipe" class="recipePreview" :recipe="r" />
          </b-col>
        </b-row>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>
export default {
  name: "vuetify-test",
  data() {
    return {
      loaded: true,
      searchWord: '',
      Results_num: "5",
      Diet: '',
      Intolerances: '',
      Cuisines: '',
      onSearch: false
    }

  },
  mounted(){
    if(onSearch){
      this.recipes = this.$root.store.lastSearch;
    }
  },
  methods:
  {
    async startSearch() {
      onSearch=true;
      try {
          const url= this.$root.store.server_domain + "/recipes/search/";
          const response = await this.axios.get(url, { params: { 
            query: this.searchWord,
            number: this.Results_num,
            diet: this.Diet,
            intolerances: this.Intolerances,
            cuisine : this.Cuisines
        }});
          const recipes = response.data;
          this.recipes = [];
          this.recipes.push(...recipes);
          this.recipes=this.recipes.slice(0,3)
          console.log(this.recipes)
          this.$root.store.lastSearch = this.recipes
        
          // this.recipes = this.recipes.slice(0,this.form.numberOfSearch)
        
        
      } catch (err) {
        console.log(err.response);
      }
      
    },
    
    getHistory() {
      console.log(this.$root.store.lastSearch) 
      if (this.$root.store.username) {
        this.searchHistory = this.$root.store.lastSearch; 
        if (this.searchHistory != [])
        {
          this.searchHistoryExists = true;
        }
      }
    },
    TimeSort(){
      this.recipes = this.recipes.sort((a,b) => a.readyInMinutes-b.readyInMinutes);    
    },
    PopolaritySort(){
      this.recipes = this.recipes.sort((a,b) => -(a.popularity-b.popularity));
    }
  },
};
</script>


<style scoped>
label textarea {
  vertical-align: middle;
}

h1 {
  font-size: 5em;
  font-family: 'Readex Pro', sans-serif;
}

.input-field {
  vertical-align: middle;
  justify-content: center;
  text-align: center;
  direction: rtl;
  border-radius: 70px;
  box-shadow: 1px 1px 3px -2px rgb(0 0 0 / 20%), 1px 1px 1px 1px rgb(0 0 0 / 14%), 1px 1px 5px 1px rgb(0 0 0 / 12%);
  width: 45%;
  padding: 1%;
  margin-top: 5%;
}

input:hover {
  outline-color: rgb(80, 80, 81);
  outline-width: 0.1px;
  box-shadow: 0px 4px 2px -2px rgb(0 0 0 / 20%), 0px 2px 2px 2px rgb(0 0 0 / 14%), 3px 3px 6px 4px rgb(0 0 0 / 12%);
}

input:focus {
  outline: none;
}

input:focus::placeholder {
  color: transparent;
}

::placeholder {
  font-size: large;
}

::placeholder:hover {
  display: none;
}

.gray{
  color: darkolivegreen;
}

</style>