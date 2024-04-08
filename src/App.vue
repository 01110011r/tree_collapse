<script>
import Tree from "@/components/tree.vue";
import rootData from "@/data.json";

export default {
  name: "app",
  data() {
    return {
      data: rootData,
    };
  },
  watch: {
    data: {
      deep: true,
      handler(newVal) {
        console.log(newVal);
      },
    },
  },
  methods: {
    nodeWasClicked(node) {
      console.log(node);
    },
  },
  components: {
    Tree,
  },
};
</script>

<template>
<template>
  <div id="app">
    <h1>
      Tree Collapse
    </h1>
    <Tree :nodes="data" @onClick="nodeWasClicked"/>
  </div>
</template>
</template>

<style scoped>

body{
  font-family: Arial, sans-serif;
  background: #2c3e50;
  color: white;
}

</style>
