

<script setup >
import { reactive, toRefs, ref } from "vue";
import vueTree from "../components/vueTree";
const props = defineProps({
  treeData: {
    default: [],
  },
  selectedKey: {
    type: Number,
    default: 0,
  },
});
const emit = defineEmits(["onExpand", "onSelect", "onExpend"]);
const timer = ref(null);
const { selectedKey } = toRefs(props);
let isLeaf = (node) => {
  return !node.children?.length;
};
const Expand = (item) => {
  item.expand = !item.expand;
  emit("onExpand", item);
};

const selectEvent = (item, ev) => {
  clearTimeout(timer.value);
  timer.value = setTimeout(() => {
    emit("onSelect", item);
  }, 0);
};
</script>
<template>
  <div class="container-Tree">
    <div
      :class="[
        isLeaf(item) ? 'Leaf' : 'ParentLeaf',
        selectedKey === item.fVcUuid ? 'active' : '',
      ]"
      class="TreeNode"
      @click.stop="selectEvent(item, $event)"
      v-for="item in treeData"
      :key="item.fVcUuid"
    >
      <button @click.stop="Expand(item)">
        <template v-if="!item.expand"> + </template>
        <template v-else>-</template>
      </button>
      {{ item.fVcName }}

      <vueTree
        @onSelect="selectEvent"
        @onExpend="Expand"
        :selectedKey="selectedKey"
        v-if="!isLeaf(item) && item.expand"
        :treeData="item.children"
      ></vueTree>
    </div>
  </div>
</template>

<style scoped lang="less">
.ParentLeaf > .container-Tree {
  margin-left: 16px;
}
.TreeNode {
  color: initial;
}
button {
  min-width: 25px;
}
.container-Tree .active {
  color: red;
}
</style>

