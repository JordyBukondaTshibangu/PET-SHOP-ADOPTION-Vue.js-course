<template>
  <div class="home">
    <h2>Adopt a new friend</h2>
    <p>Number of Pets : {{animalsCount}}</p>
    <p>Number of Cats : {{getAllCats.length}}</p>
    <button class="btn btn-primary" @click="toggleShowPetForm">Add New Pet</button>
<b-form @submit.prevent="handleSubmit"  v-if="showPetForm">
      <b-form-group id="input-group-1" label="Pet Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          type = "text"
          v-model="form.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Species:" label-for="input-2">
        <b-form-select
          id="input-2"
          v-model="form.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-3" label="Pet Age:" label-for="input-3">
        <b-form-input
          id="input-3"
          type="number"
          v-model="form.age"
          required
          placeholder="Enter Age"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: "Home",
  data(){
    return {
      showPetForm : false,
      form : {
        name : '',
        species : null,
        age : 0
      }
    }
  },
  methods : {
    ...mapActions(['addPet']),
    toggleShowPetForm(){
      this.showPetForm = !this.showPetForm
    },
    handleSubmit(){
      const { species, name, age } = this.form 
      const payload = {
        species ,
        pet : {
          name,
          age
        }
      }
      this.addPet(payload)
      this.form =  {
        name : '',
        species : null,
        age : 0
      }
    }
  },
  computed : {
    ...mapGetters(['animalsCount', 'getAllCats'])
  }
};
</script>
