<template>
  <el-tree
    :data="menus"
    :props="defaultProps"
    node-key="catId"
    show-checkbox
    :expand-on-click-node="false"
  >
    <span class="custom-tree-node" slot-scope="{ node, data }">
      <span>{{ node.label }}</span>
      <span>
        <el-button v-if="node.level <= 2" type="text" size="mini" @click="() => append(data)">
          Append
        </el-button>
        <el-button v-if="node.childNodes.length == 0" type="text" size="mini" @click="() => remove(node, data)">
          Delete
        </el-button>
      </span>
    </span>
  </el-tree>
</template>

<script>
export default {
  data() {
    return {
      menus: [],
      defaultProps: {
        children: "children",
        label: "name",
      },
    };
  },
  methods: {
    // 获取数据列表
    getMenus() {
      this.$http({
        url: this.$http.adornUrl("/product/category/list/tree"),
        method: "get",
      }).then(({ data }) => {
        this.menus = data.data;
      });
    },
    append(data) {
      console.log("append", data)
    },

    remove(node, data) {
      console.log("remove", node, data)
    },
  },
  // 创建完成(可以访问到当前this实例)
  created() {
    this.getMenus();
  },
};
</script>

<style>
</style>