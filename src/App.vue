<template>
  <div id="app">
    <tree class="node-tree" :data="treeData" @make-folder="makeFolder" @add-node="addNode"></tree>
  </div>
</template>

<script>
import Tree from "./components/Tree.vue"

export default {
  name: 'App',
  components: {
    Tree,
  },
  data() {
    return {
      treeData: {
        name: "My Tree",
        children: [
          { name: "hello" },
          { name: "wat" },
          {
            name: "child folder",
            children: [
              {
                name: "child folder",
                children: [{ name: "hello" }, { name: "wat" }]
              },
              { name: "hello" },
              { name: "wat" },
              {
                name: "child folder",
                children: [{ name: "hello" }, { name: "wat" }]
              }
            ]
          }
        ]
      }
    }
  },
  methods: {
    makeFolder(node) {
      this.$set(node, "children", []);
      this.addNode(node);
    },
    addNode(node) {
      node.children.push({
        name: "new stuff"
      })
    }
  }
}
</script>

<style>
body {
  font-family: Menlo, Consolas, monospace;
  color: #444;
}
.node-tree {
  cursor: pointer;
}

.bold {
  font-weight: bold;
}

ul {
  padding-left: 1em;
  line-height: 1.5em;
  list-style-type: dot;
}
</style>
