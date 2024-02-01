<template>
  <Tree :categories="categories" />
</template>

<script>
import Tree from './components/Tree.vue'

export default {
  name: 'App',
  data() {
    return {
      categories: [
        { id: '1', name: 'Lorem', children: [
            { id: '2', name: 'Ipsum', children: [] },
            { id: '3', name: 'Dolor', children: [
                { id: '4', name: 'Sit', children: [] }
              ] }
          ] }
      ]
    }
  },
  components: {
    Tree
  }
}
</script>