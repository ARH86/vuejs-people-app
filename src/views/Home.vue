<template>
  <div class="home">
    <h1>Interesting People</h1>
      <ul>
        <li v-for="error in errors">{{ error }}</li>
      </ul>
    <div>
      Name: <input v-model="newPerson.name">  
      Bio: <input v-model="newPerson.bio">
      <button v-on:click="addPerson()">Add Person</button>
    </div>

    <div>
      <h4>Total Number of People: {{ people.length }}</h4>
    </div>

    <div v-for="person in people">
      <h2 @click="toggleBio(person)">{{ person.name }}</h2>
      <div v-bind:class="{strike: person.bioVisible}">  
        <h3>{{ person.bio }}</h3>
      <button @click="deletePerson(person)">Delete</button>
      </div>
    </div>
  </div>
</template>

<style>
  .strike {
      text-decoration: line-through;

  }

</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      people: [],

      newPerson: {name: "", bio: "", bioVisible: false},

      errors: []


    };
  },
  created: function() {
    axios.get("http://localhost:3000/api/people")
    .then(response => { 
      this.people = (response.data);
    });
  },
  methods: {
    toggleBio: function(inputPerson) {
      inputPerson.bioVisible = !inputPerson.bioVisible;
    },
    addPerson: function() {
      this.errors = [];
        var params = {
                      name: this.newPerson.name,
                      bio: this.newPerson.bio 
                      };


        axios
        .post("http://localhost:3000/api/people", params)
        .then(response => {
          this.people.push(response.data);
        this.newPerson = {name: "", bio: "", bioVisible: false};
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });

    
      
    },
    deletePerson: function(inputPerson) {
      var index = this.people.indexOf(inputPerson);
      this.people.splice(index, 1);
    }
  },
  computed: {}
};
</script>


















