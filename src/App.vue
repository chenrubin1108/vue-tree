<template>
  <vueTree
    v-if="treeData.length != 0"
    @onSelect="selectEvent"
    @onExpand="expandEvent"
    :selectedKey="activeKey"
    :treeData="treeData"
  ></vueTree>
</template>

<script>
import { reactive, toRefs, ref, defineComponent } from "vue";
import vueTree from "./components/vueTree.vue";
export default defineComponent({
  components: {
    vueTree,
  },
  setup() {
    let activeKey = ref(null);
    let treeData = reactive([
      {
        fVcName: "chenrubin",
        fVcUuid: 1,
        children: [
          {
            fVcName: "张三",
            fVcUuid: 2,
            children: [
              {
                fVcName: "儿子",
                fVcUuid: 9,
                children: [
                  {
                    fVcName: "儿子66",
                    fVcUuid: 12,
                  },
                ],
              },
            ],
          },
          {
            fVcName: "678111",
            fVcUuid: 3,
            children: [],
          },
        ],
      },
      {
        fVcName: "binbin",
        fVcUuid: 4,
        children: [],
      },
    ]);
    let selectEvent = (node) => {
      activeKey.value = node.fVcUuid;
    };
    let expandEvent = () => {
      console.log("扩展事件");
    };
    return { expandEvent, activeKey, selectEvent, treeData };
  },
});
</script>

<style>
</style>
