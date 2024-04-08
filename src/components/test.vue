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

    }
  }
}
</script>

<template>
  <draggable class="drag-area" tag="div">
    <div
        v-for="node in nodes"
        :key="node.name"

        :style="{'margin-left': `${depth * 20}px`}"
        class="node"
    >
      <span class="type" @click="nodeClicked(node)">{{isExpanded(node) ? '&#9660;' : '&#9658;'}}</span>
      <span class="type">&#9671;</span>
      <span :style="getStyle(node)">{{node.name}}</span>
      <Tree v-if="isExpanded(node) && node.children"
            :nodes="node.children"
            :depth="depth + 1"
            @onClick="(node) => $emit('onClick', node)"
      />
    </div>
  </draggable>
</template>

<style scoped>

</style>