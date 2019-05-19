<template>
  <div id="app">
      <b-container>
        <b-row>
          <b-col></b-col>
          <b-col cols="8">
            <h1>Argparse builder</h1>

            <b-form-textarea
              id="textarea"
              v-model="description"
              placeholder="You can add a description for the whole parser..."
              rows="3"
              max-rows="6"
            ></b-form-textarea>

            <h2>Arguments</h2>
            <ul>
              <li :key="arg.id" v-for="arg in args">
                {{ arg.name }} - {{ arg.position }}
                <b-button type="button" v-on:click="remove_argument(arg.id)">-</b-button>
              </li>
            </ul>

            <h2>Add a new argument</h2>
            <b-form-input v-model="name" placeholder="Argument name"></b-form-input>
            <select v-model="position">
                <option value="positional">Positional</option>
                <option value="optional">Optional</option>
            </select> 
            <b-dropdown id="dropdown-1" text="Dropdown Button" class="m-md-2">
              <b-dropdown-item>First Action</b-dropdown-item>
              <b-dropdown-item>Second Action</b-dropdown-item>
              <b-dropdown-item>Third Action</b-dropdown-item>
              <b-dropdown-divider></b-dropdown-divider>
              <b-dropdown-item active>Active action</b-dropdown-item>
              <b-dropdown-item disabled>Disabled action</b-dropdown-item>
            </b-dropdown>
            <b-button variant="outline-primary" type="button" v-on:click="add_argument">+</b-button>
            
            <preview :description="description" :args="args"></preview>            
          </b-col>
          <b-col></b-col>
        </b-row>
      </b-container>
  </div>
</template>

<script>
import Preview from './components/Preview.vue'

export default {
  name: 'app',
  components: {
    Preview
  },
  data() {
    return {
      args: [],
      name: '',
      position: '',
      description: '',
    };
  },
  methods: {
    add_argument: function() {
      this.args.push({
        'id': Date.now(),
        'name': this.name,
        'position': this.position
      });
    },

    remove_argument: function(id) {
      this.args = this.args.filter(function(e) { return e.id !== id })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
