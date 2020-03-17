<template>
  <div class="home">
    <h1>Adopt a new Best Friend.</h1> 
    <h3>Total pets: {{ animalsCount }} </h3>
    <button v-on:click="togglePetForm" class="btn btn-primary">Add New Pet</button>
    <div class="form">
          <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
       
          <b-form-group id="input-group-1" label="Pet's Name:" label-for="input-1">
            <b-form-input
              id="input-1"
              v-model="formData.name"
              required
              placeholder="Enter name"
            ></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-2" label="Species:" label-for="input-2">
            <b-form-select
              id="input-2"
              v-model="formData.species"
              :options="['cats','dogs']"
              required
            ></b-form-select>
          </b-form-group>

           <b-form-group id="input-group-3" label="Pet's age:" label-for="input-3">
            <b-form-input
              id="input-3"
              v-model="formData.age"
              type="number"
              required
              placeholder="Enter age"
            ></b-form-input>
          </b-form-group>
     

          <b-button class="form-btn" type="submit" variant="primary">Submit</b-button>
          <b-button class="form-btn" type="reset" variant="danger">Reset</b-button>
        </b-form>
        <!-- <b-card class="mt-3" header="Form Data Result">
          <pre class="m-0">{{ form }}</pre>
        </b-card> -->
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {

  name: "Home",
  data() {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age:0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount'
    ])
  },
  methods: {
    ...mapActions ([
        'addPet'
    ]),
    togglePetForm() {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit() {
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)

      // reset form fields after submit 
      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
};
</script>

<style scoped>
  .btn {
    margin-bottom: 40px;
    margin-top: 30px;
  }

  .form-btn {
    margin-right: 20px;
  }

  .form {
    max-width: 450px;
    margin: auto;
  }
</style>
