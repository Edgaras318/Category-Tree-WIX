<template>
  <ul>
    <li v-for="node in nodes" :key="node.id" :style="{ marginLeft: `${node.depth * 20}px` }">
      {{ node.name }}
      <button @click="addChild(node)">Add Child</button>
      <iterative-tree-node :nodes="node.children" v-if="node.children && node.children.length > 0" @addNode="addChild"/>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'IterativeTreeNode',
  components: {
    'iterative-tree-node': () => import('./IterativeTreeNode.vue') // Recursive component
  },
  props: {
    nodes: {
      type: Array,
      required: true
    },
  },
  methods: {
    addChild(node) {
      this.$emit('AddNode', node)
    }
  }
}
</script>

<style scoped>
li {
  margin-bottom: 5px;
}
</style>
