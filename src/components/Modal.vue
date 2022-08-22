<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <slot name="header">Create Recipe</slot>
          </div>

          <div class="modal-body">
            <form id="contact-form">
              <div class="form-group">
                <input id="Recipe name" class="form-control" type="text" name="name" placeholder="Recipe name"/>
              </div>
              <div class="form-group">
                <textarea class="form-control" id="description" placeholder="Short description" rows="1"></textarea>
              </div>
              <div class="form-group">
                <textarea class="form-control" id="Ingredient" placeholder="Ingredient list" rows="3"></textarea>
              </div>
              <div class="form-group">
                <textarea class="form-control" id="Instructions" placeholder="Instructions" rows="3"></textarea>
              </div>
              <div class="form-group">
                <label style="width:100px;display:inline-block;">Time</label>
                <input id="Time" type="number" name="Time" min="1" max="500">
              </div>

              <div class="form-group">
                <input id="Vegeterian" type='checkbox' name='system_type17' value='2' />
                <span style="width:100px;display:inline-block;">Vegeterian</span>
                <input id="Gluten" type='checkbox' name='system_type17' value='2' />
                <span style="width:100px;display:inline-block;">Gluten Free</span>
                <input id="Vegan" type='checkbox' name='system_type17' value='2' />
                <span style="width:100px;display:inline-block;">Vegan</span>
              </div>    
              <div class="form-group">
                <span style="width:100px;display:inline-block;">Serving</span>
                <input id="Serving" type="number" name="Serving" min="1" max="100">
              </div>

              <div class="form-group">
                <label for="exampleFormControlFile1">Recipe image</label>
                <input type="file" class="form-control-file" id="image">
              </div>
              <button @click="submit_btn" type="submit" class="btn btn-primary">Submit</button>
            </form>
          </div>

          <div class="modal-footer">
            <slot name="footer">
              default footer
              <button
                class="modal-default-button"
                @click="$emit('close')"
              >OK</button>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
import { METHODS } from 'http';

export default {
  props: {
    show: Boolean
  },
  data() {
    return{
      errors: [],
      name: null,
      description: null,
      Instructions: null,
      Time: 1,
      Gluten: false,
      Vegan: false,
      Vegeterian: false,
      Serving: 0,
      image: null,
      Ingredient: null
    }
  },
  methods:{
    async submit_btn(){
      console.log("!");
      this.name = document.getElementById("Recipe name").value;
      this.description = document.getElementById("description").value;
      this.Instructions = document.getElementById("Instructions").value;
      this.Time = document.getElementById("Time").value;
      this.Serving = document.getElementById("Serving").value;
      this.image = document.getElementById("image").value;

      if(document.getElementById("Vegeterian").checked = true){ this.Vegeterian=true; }
      if(document.getElementById("Vegan").checked = true){ this.Vegan=true;}
      if(document.getElementById("Gluten").checked = true){ this.Gluten=true;}
      
      console.log("--------------------------------");
      console.log(this.name);
      console.log(this.description);
      console.log(this.Instructions);
      console.log(this.Gluten);
      console.log(this.Vegeterian);
      console.log(this.Serving);
      console.log(this.image);
      console.log(this.Ingredient);

      console.log("2");

      const response = await this.axios.post(
        this.$root.store.server_domain + "/users/myRecipes",
        {
            title: this.name,
            readyInMinutes: this.Time,
            image: this.image,
            vegan: this.Vegan,
            vegetarian: this.Vegeterian,
            glutenFree: this.Gluten,
            servings: this.Serving,
            extendedIngredients: this.description,
            instructions: this.Instructions
        }
      );

    }
  },
  mounted(){
    console.log("2");


  }
}



function callbackFunction(event) {
    event.preventDefault();
    const myFormData = new FormData(event.target);
    console.log(myFormData);
}
</script>


<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
  
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
      overflow-y: initial !important

}

.modal-container {
  width: 500px;
  margin: 0px auto;
  padding: 5px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;

  
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 5px 0;
  height: 65vh;
  overflow-y: auto;
}

.modal-default-button {
  float: right;
}


.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>