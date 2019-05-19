<template>
  <div id="preview">
    <import></import><br>
    parser = argparse.ArgumentParser(description='{{ description }}')<br>
    <p v-for="arg in args" :key="arg.id">
      <template v-if="arg.position == 'positional'">
        parser.add_argument('{{ arg.name }}')
      </template>
      <template v-else>
        parser.add_argument('--{{ arg.name }}', '-{{ arg.name[0] }}')
      </template>
    </p><br>
    args = parser.parse_args()
  </div>
</template>

<script>
import Import from './Import.vue'

export default {
  name: 'HelloWorld',
  props: ['description', 'args'],
  components: {
    Import
  }
}
</script>

<style scoped>
#preview {
  background-color: #e9ecef;
  padding: 5px;
}
</style>
