<template>
  <div>
    <h2>Recursive Tree</h2>
    <ul>
      <recursive-tree-node :node="rootNode" @addNode="addChild" />
    </ul>

    <h2>Iterative Tree</h2>
    <ul>
      <iterative-tree-node :nodes="iterativeNodes" @addNode="addChild"/>
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
  computed: {
    iterativeNodes() {
      const queue = [{ node: this.rootNode, depth: 0 }]
      const result = []

      while (queue.length > 0) {
        const { node, depth } = queue.shift()

        result.push({ id: node.id, name: node.name, depth, children: node.children })
      }
      return result
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
