<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <slot name="header">Create Recipe</slot>
          </div>

    <b-form @submit.prevent="onRegister" @reset.prevent="onReset" @addPhoto.prevent="onPic">
      <b-form-group
        id="input-group-title"
        label-cols-sm="3"
        label="title:"
        label-for="title"
      >
        <b-form-input
          id="title"
          v-model="$v.form.title.$model"
          type="text"
          :state="validateState('title')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.title.required">
          title is required
        </b-form-invalid-feedback>
        <b-form-invalid-feedback v-if="!$v.form.title.alpha">
          title should contain only letters
        </b-form-invalid-feedback>
      </b-form-group>
    
      <b-form-group
        id="input-group-description"
        label-cols-sm="3"
        label="description:"
        label-for="description"
      >
        <b-form-input
          id="description"
          v-model="$v.form.description.$model"
          type="text"
          :state="validateState('description')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.description.required">
          description is required
        </b-form-invalid-feedback>
      </b-form-group>
 
      <b-form-group
        id="input-group-Instructions"
        label-cols-sm="3"
        label="Instructions:"
        label-for="Instructions"
      >
        <b-form-input
          id="Instructions"
          v-model="$v.form.Instructions.$model"
          type="text"
          :state="validateState('Instructions')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.Instructions.required">
          Instructions is required
        </b-form-invalid-feedback>
      </b-form-group>

      <b-form-group
        id="input-group-extendedIngredients"
        label-cols-sm="3"
        label="extendedIngredients:"
        label-for="extendedIngredients"
      >
        <b-form-input
          id="extendedIngredients"
          v-model="$v.form.extendedIngredients.$model"
          type="text"
          :state="validateState('extendedIngredients')"
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-readyInMinutes"
        label-cols-sm="3"
        label="readyInMinutes:"
        label-for="readyInMinutes"
      >
        <b-form-input
          id="readyInMinutes"
          v-model="$v.form.readyInMinutes.$model"
          type="text"
          :state="validateState('readyInMinutes')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.readyInMinutes.required">
          readyInMinutes is required
        </b-form-invalid-feedback>
      </b-form-group>

      <b-form-group
        id="input-group-Serving"
        label-cols-sm="3"
        label="Serving:"
        label-for="Serving"
      >
        <b-form-input
          id="Serving"
          v-model="$v.form.Serving.$model"
          type="Serving"
          :state="validateState('Serving')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.Serving.required">
          Serving is required
        </b-form-invalid-feedback>
      </b-form-group>

      <b-form-group
        id="input-group-Ingredient"
        label-cols-sm="3"
        label="Ingredient:"
        label-for="Ingredient"
      >
        <b-form-input
          id="Ingredient"
          type="Ingredient"
          v-model="$v.form.Ingredient.$model"
          :state="validateState('Ingredient')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.Ingredient.required">
          Ingredient is required
        </b-form-invalid-feedback>
      
      <b-form-file
          id="image"
          type="text"
          v-model="$v.form.image.$model"
          :state="validateState('image')"
          placeholder="choose file"
          drop-placeholder="Drop here"
          accept="image/*"
          class="form-control"
        ></b-form-file>


      </b-form-group>
      <b-form-group>
        <input type="checkbox" id="Vegeterian" class="unchecked" name="Vegeterian" ref="Vegeterian">
        <label for="Vegeterian">Vegeterian</label>
        <input type="checkbox" id="Vegan" class="unchecked" name="Vegan" ref="Vegan">
        <label for="Vegan">Vegan</label>
        <input type="checkbox" id="glutenFree" class="unchecked" name="glutenFree" ref="glutenFree">
        <label for="glutenFree">Gluten Free</label>
      </b-form-group>

      <b-button type="reset" variant="danger">Reset</b-button>
      <b-button
        type="submit"
        variant="primary"
        style="width:250px;"
        class="ml-5 w-75 btn-submit"
        >Submit</b-button
      >
      </b-form>

      <div class="modal-footer">
        <button
          class="modal-default-button"
          @click="$emit('close')"
        >Close</button>
      </div>

        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
import {
  required,
  alpha
} from "vuelidate/lib/validators";

export default {
  props: {
    show: Boolean
  },
  data() {
    return{
      form: {
        title: "",
        description: "",
        Instructions: "",
        glutenFree: false,
        Vegan: false,
        Vegeterian: false,
        extendedIngredients: "",
        readyInMinutes: 0,
        Serving: 0,
        Ingredient: "",
        submitError: undefined,
        image: ""
      },
      validated: false
    }
  },
  validations: {
    form: {
      title: {
        required,
        alpha
      },
      description:{
        required,
      },
      Instructions:{
        required,
      },
      readyInMinutes:{
        required,
        Number
      },
      Serving:{
        required,
        Number
      },
      Ingredient: {
        required
      },
      extendedIngredients:{

      },
      image:{

      }
    }
  },
  methods:{
    onRegister() {
      // console.log("register method called");
      this.$v.form.$touch();
      if (this.$v.form.$anyError) {
        return;
      }
      //console.log("register method go");
      this.Register();
    },
    onReset() {
      this.form = {
        title: "",
        description: "",
        Instructions: "",
        extendedIngredients: "",
        glutenFree: false,
        Vegan: false,
        Vegeterian: false,
        readyInMinutes: 0,
        Serving: 0,
        Ingredient: "",
        image: ""
      };
      this.$nextTick(() => {
        this.$v.$reset();
      });
    },
    validateState(param) {
      const { $dirty, $error } = this.$v.form[param];
      return $dirty ? !$error : null;
    },
    async Register() {
      try {
        if(document.getElementById("Vegeterian").checked){
          this.form.Vegeterian = true;
        }
        if(document.getElementById("vegan").checked){
          this.form.vegan = true;
        }
         if(document.getElementById("glutenFree").checked){
          this.form.glutenFree = true;
        }


        const response = await this.axios.post(
          // "https://test-for-3-2.herokuapp.com/user/Register",
          this.$root.store.server_domain + "/users/myRecipes",
          {
            title: this.form.title,
            description: this.form.description,
            instructions: this.form.Instructions,
            extendedIngredients: this.form.extendedIngredients, 
            readyInMinutes: this.form.readyInMinutes, //int
            servings: this.form.Serving, //int
            Ingredient: this.form.Ingredient, //bool
            glutenFree: this.form.glutenFree, //bool
            vegan: this.form.vegan, //bool
            vegetarian: this.form.vegetarian,
            image : this.form.image
          },
          
        );
      } catch (err) {
        //console.log(err.response);
        this.form.submitError = err.response.data.message;
      }
    },
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