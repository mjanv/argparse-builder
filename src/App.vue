<template>
  <div id="app">

      <nav class="navbar navbar-light bg-light navbar-dark bg-dark">
        <span class="navbar-brand mb-0 h1">Argparse builder</span>
        <button class="btn btn-outline-secondary my-2 my-sm-0" type="submit">Fork me on Github</button>
      </nav>

      <b-container>

        <div class="jumbotron jumbotron-fluid">
          <div class="container">
            <h1 class="display-4">Tired of writing python arguments parser ?</h1>
            <p class="lead">...</p>
          </div>
        </div>

        <b-row>
          <b-col>
            <h2>Parser</h2>
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
            <select class="custom-select" v-model="position">
                <option selected>Choose...</option>
                <option value="positional">Positional</option>
                <option value="optional">Optional</option>
            </select>
            <b-button variant="outline-primary" type="button" v-on:click="add_argument">+</b-button>
          </b-col>
          <b-col>
            <preview :description="description" :args="args"></preview>
            <!--<pre v-highlightjs><code class="python"></code></pre>-->
          </b-col>
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
}
</style>
