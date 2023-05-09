<template>
  <div id="container">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
      <RouterView/>
    </nav>
  </div>

  <div class="wrapper">
    <form @submit.prevent="addItem" autocomplete="off">
      <h1>Kegiatan</h1>
      <label> Kegiatan Kamu: {{ isComplete }} / {{ totalItems }}</label>
      <div class="task">
      <input
        type="text"
        class="task-input"
        v-model="newItem"
        placeholder="Masukkan Kegiatan"
      />
        
        <button  class="button btn-add">Tambah Kegiatan</button>
    </div>
    
   
    <ul class="task-list">
    
      <li class="task-list-item" 
      v-for="(item, index) in items" :key="index" v-bind:class="{completed: item.completed}">
          <input type="checkbox" 
          v-model="item.completed"/>
          <span>{{ item.text }}</span>
        <!-- delete item on click-->
        <button v-on:click= "deleteItem(index)"
          class="button btn-delete">Hapus</button>
      </li>
    </ul>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: "",
      items: [], 
    };
  },
  computed: {
    totalItems() {
      return this.items.length;
    },
    isComplete() {
      return this.items.filter(item => item.completed).length; 
    }
  },
  methods: {
    addItem() {
      if (this.newItem !== "") {
        this.items.push({text: this.newItem, completed: false}); 
        this.newItem = ""; 
      }
    },
    deleteItem(index) {
      this.items.splice(index, 1); 
    }
  },
};
</script>

<style lang="scss">
@import "src/assets/to-do.scss";
</style>