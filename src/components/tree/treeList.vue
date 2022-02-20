<template>
  <div>
    <div class="tree-list" v-for="(item, key) in data" :key="key">
      <div :class="active===item.name?'active':''">{{ item.name }}</div>
      <tree-list
        v-if="item.children && item.children.length>0"
        :active="active"
        :data="item.children"
      />
    </div>
  </div>
</template>
<script>

export default {
  name: "treeList",
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    active:{
        type:String,
        default:''
    }
  },
  watch:{
      active(newVal){
          console.log(11,newVal)
      }
  },
  data() {
    return {};
  },
};
</script>
<style scoped>
.tree-list {
  margin-left: 10px;
}
.tree-list .active{
    background: red;
    color:#ffffff;
}
</style>



