<template>
  <ul>
    <li v-for="node in iterativeNodes" :key="node.id" :style="{ marginLeft: `${node.depth * 20}px` }">
      {{ node.name }}
      <button @click="addChild(node)">Add Child</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'IterativeTreeNode',
  props: {
    nodes: {
      type: Object,
      required: true
    },
  },
  methods: {
    addChild(node) {
      this.$emit('addNode', node);
    }
  },
  computed: {
    iterativeNodes() {
      const result = [];
      const stack = [{ node: this.nodes, depth: 0 }];

      while (stack.length > 0) {
        const { node, depth } = stack.pop();
        result.push({ ...node, depth });

        // Add children to the stack in reverse order to mimic desired rendering order
        if (node.children && node.children.length > 0) {
          for (let i = node.children.length - 1; i >= 0; i--) {
            stack.push({ node: node.children[i], depth: depth + 1 });
          }
        }
      }

      return result
    }
  }
}
</script>

<style scoped>
li {
  margin-bottom: 5px;
}
</style>
