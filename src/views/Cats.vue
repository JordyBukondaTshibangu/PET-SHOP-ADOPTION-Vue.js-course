<template>
  <div class="home">
    <h3>Cats for adoption</h3>
    <b-table striped hover :items="cats">
      <template v-slot:cell(name)="data">
        <router-link :to="`/pets/cats/${data.index}`">{{ data.value }}</router-link>
      </template>
    </b-table>
  </div>
</template>

<script>
import { mapState } from 'vuex'
  export default {
    computed : {
      ...mapState([
        'cats'
      ])
    }
  }
</script>
