<template>
  <div class="tab-control">
    <div
      v-for="(item , index) in titles"
      :key="index"
      class="tab-item"
      :class="{Active:currentIndex===index}"
      @click="itemClick(index)"
    >
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabControl",
  props: {
    titles: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      currentIndex: 0,
    };
  },
  methods:{
    itemClick(index){
      this.currentIndex = index
    }
  }
};
</script>

<style scoped>
.tab-control {
  display: flex;
  text-align: center;
  background-color: #fff;
  font-size: 15px;
  height: 44px;
  line-height: 44px;
  position: sticky;
  top: 44px;
}
.tab-item {
  flex: 1;
}
.tab-item span {
    padding: 5px;
}


.Active {
  color: var(--color-high-text);
}
.Active span{
 border-bottom: 3px solid var(--color-tint);
}
</style>