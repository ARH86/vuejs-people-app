<template>
  <div class="home">
    <h1> People </h1>
  </div>
  <div>
    <input v-model="newPerson.text">
    <button v-on:click="addPerson()">Add Person</button>
  </div>
  <div>
    
  </div>
</template>

<style>
</style>

<script>
export default {
  data: function() {
    return {
      bio: [
          {name: "Joe", bio:"Born in a sahara desert ", bioVisible: true },
          {name: "Dill", bio:"Never had a parent ", bioVisible: true },
          {name: "Garlin", bio:"Lives his life spicy", bioVisible: true }
      ],
      newPerson: {name: '', bio: '', bioVisible: truep}
    };
  },
  created: function() {},
  methods: {},
  computed: {}
};
</script>