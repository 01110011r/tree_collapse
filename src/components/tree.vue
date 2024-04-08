
<template>
  <draggable class="drag-area" tag="div" :list="nodes">
    <div
    v-for="node in nodes"
    :key="node.name"

    :style="{'margin-left': `${depth * 20}px`}"
    class="node"
    >
      <span class="type" @click="nodeClicked(node)">{{isExpanded(node) ? '&#9660;' : '&#9658;'}}</span>
      <span class="type">&#9671;</span>
      <span>{{node.name}}</span>
      <Tree v-if="isExpanded(node) && node.children"
            :nodes="node.children"
            :depth="depth + 1"
            @onClick="(node) => $emit('onClick', node)"
            />
    </div>
  </draggable>
</template>

<script>
import draggable from 'vuedraggable';
export default {
  name: 'Tree',
  props: {
    nodes: Array,
    depth: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      expanded: [],
    };
  },
  methods:{
    isExpanded(node) {
      return this.expanded.includes(node);
    },
    nodeClicked(node) {
      if(!this.isExpanded(node)){
        this.expanded.push(node);
      } else {
        this.expanded.splice(this.expanded.insexOf(node));
      }
    },

  },
  components: {
    draggable,
  },
  computed: {},
};
</script>


<style scoped>
.node {
  text-align: left;
  font-size: 18px;
}

.type {
  margin-right: 10px;
}
</style>