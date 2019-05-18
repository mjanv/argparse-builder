<template>
  <div id="app">
      <p>Argparse builder</p>

      <textarea v-model="description" placeholder="Parser description"></textarea>
      <p>Arguments</p>
      <ul>
        <li :key="arg.id" v-for="arg in args">
          {{ arg.name }} - {{ arg.position }}
          <button type="button" v-on:click="remove_argument(arg.id)">-</button>
        </li>
      </ul>
      <input v-model="name" placeholder="name">
      <select v-model="position">
          <option value="positional">Positional</option>
          <option value="optional">Optional</option>
      </select> 
      <button type="button" v-on:click="add_argument">+</button>
      <preview :description="description" :args="args"></preview>
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
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
