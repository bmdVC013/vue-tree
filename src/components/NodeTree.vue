<template>
  <li>
    <div
      :class="{bold: isFolder}"
      @click="toggle"
      @dblclick="makeFolder"
    >
      {{ node.name }}
      <span v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
    </div>

    <ul v-show="isOpen" v-if="isFolder">
      <node
        class="node-tree"
        v-for="(child, index) in node.children"
        :key="index"
        :node="child"
        @make-folder="$emit('make-folder', $event)"
        @add-node="$emit('add-node', $event)"
      ></node>
      <li class="add" @click="$emit('add-node', node)">+</li>
    </ul>
  </li>
</template>

<script>
export default {
  name: 'Node',
  props: {
    node: {
      type: Object,
      required: false,
      default: () => ({}),
    }
  },
  data() {
    return {
      isOpen: false,
    }
  },
  computed: {
    isFolder() {
      return this.node.children && this.node.children.length;
    }
  },
  methods: {
    toggle() {
      if (this.isFolder) {
        this.isOpen = !this.isOpen;
      }
    },
    makeFolder() {
      if (!this.isFolder) {
        this.$emit('make-folder', this.node);
        this.isOpen = true;
      }
    }
  }
}
</script>
