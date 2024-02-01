<template>
  <div>
    <h2>Recursive Tree</h2>
    <ul>
      <recursive-tree-node :node="rootNode" @addNode="addChild" />
    </ul>

    <h2>Iterative Tree</h2>
    <ul>
      <iterative-tree-node :nodes="rootNode" @addNode="addChild"/>
    </ul>
  </div>
</template>

<script>
import RecursiveTreeNode from './RecursiveTreeNode.vue'
import IterativeTreeNode from './IterativeTreeNode.vue'

export default {
  name: 'Tree',
  components: {
    'recursive-tree-node': RecursiveTreeNode,
    'iterative-tree-node': IterativeTreeNode
  },
  props: {
    categories: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      rootNode: {
        id: 'root',
        name: 'Root',
        children: this.categories
      }
    }
  },
  methods: {
    addChild(node) {
      const name = prompt('Enter child name')
      if (name) {
        const newNode = { id: Date.now().toString(), name, children: [] }
        node.children.push(newNode)
      }
    }
  }
}
</script>
