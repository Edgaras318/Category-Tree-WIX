<!-- RecursiveTreeNode.vue -->
<template>
  <div>
    <li :style="{ marginLeft: `${node.depth * 20}px` }">
      {{ node.name }}

      <button @click="addChild(node)">Add Child</button>
    </li>
    <ul v-if="node.children.length > 0">
      <recursive-tree-node v-for="child in node.children" :node="child" :key="child.id" @addNode="addChild"/>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'RecursiveTreeNode',
  props: {
    node: {
      type: Object,
      required: true
    }
  },
  methods: {
    addChild(node) {
      this.$emit('AddNode', node)
    }
  }
}
</script>