<template>
  <div class="list">
    <div class="item" :key="index" v-for="(item,index) in news"
     @mouseover="currentIndex = index"
     @mouseout="currentIndex = null">
      <span class="edit-btn" 
        v-show="currentIndex == index"
        @click="$emit('edit', index)">Edit</span>
      <img :src="item.img" alt="">
      <h3>{{item.title}}</h3>
      <p>{{item.content}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'list',
  props: ['news'],
  data() {
    return {
      currentIndex: null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.item {
  width: 350px;
  background: #fff;
  border: 1px #dadada solid;
  padding: 15px;
  position: relative;
  cursor: pointer;
  margin-bottom: 20px;
}
.item img {
  width: 100%;
}
.item .edit-btn {
  color: #fff;
  background: rgba(0,0,0,.6);
  position: absolute;
  padding: 7px 20px;
  border-radius: 2px;
  top: 0;
  right: 0;
}
.item h3 {
  font-size: 14px;
}
.item p {
  font-size: 12px;
}
</style>
