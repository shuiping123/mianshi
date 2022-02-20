<template>
  <div id="app">
    <input type="text" v-model="searchInp">
    <button type="button" @click="searchFun">查询</button>
    <button type="button" @click="preFun">上一条</button>
    <button type="button" @click="nextFun">下一条</button>
    <tree-list :data="data" :active="this.result.length>0&&active!==-1?result[active].name:''"/>
  </div>
</template>

<script>
import treeList from '@/components/tree/treeList'
export default {
  name: "App",
  components:{treeList},
  data() {
    return {
      searchInp:'',
      result:[],
      active:0,
      data: [
        {
          name: "name1",
          children: [
            {
              name: "name1-1",
              children: [{ name: "name1-1-1" }, { name: "name1-1-2" }],
            },
            { name: "name1-2" },
          ],
        },
        {
          name: "name2",
          children: [
            {
              name: "name2-1",
              children: [{ name: "name2-1-1" }, { name: "name2-1-2" }],
            },
            { name: "name2-2" },
          ],
        },
      ],
    };
  },
  methods: {
    searchTree(data,name){
      if(!name) return false;
      data.map(item=>{
        if(item.name.indexOf(name)!==-1){
          this.result.push(item);
        }
        if(item.children&&item.children.length>0){
          this.searchTree(item.children,name);
        }
      })
    },
    searchFun(){
      this.result=[];
      this.searchTree(this.data,this.searchInp);
      this.active=this.result.length>0?0:-1;
    },
    preFun(){
      if(this.result.length>0&&this.active!==0){
        this.active-=1;
      }
    },
    nextFun(){
      if(this.result.length>0&&this.active!==this.result.length-1){
        this.active+=1;
      }
    },
  },
};
</script>

<style>

</style>
