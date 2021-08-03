<template>
  <div class="tree">
    <ul class="tree-list">
      <node-tree
        :node="data"
        @make-folder="$emit('make-folder', $event)"
        @add-node="$emit('add-node', $event)"
      ></node-tree>
    </ul>
  </div>
</template>

<script>
import NodeTree from "./NodeTree.vue"

export default {
  name: 'Tree',
  components: {
    NodeTree
  },
  props: {
    data: {
      type: Object,
      required: false,
      default: () => ({})
    }
  }
}
</script>
