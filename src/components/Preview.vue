<template>
  <div>
    import argparse<br>
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
export default {
  name: 'HelloWorld',
  props: ['description', 'args'],
}
</script>

<style scoped>
</style>
