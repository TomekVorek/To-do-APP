<template>
<div id="container">
  <div class="item">
    <h1>Nowe To-Do: {{newItem}}</h1>
    <input type="text" placeholder="todo" v-model="newItem">
    <button @click='addItem'>Dodaj</button>
  </div> 
  
  <div 
  class="item" 
  v-for="item in items" 
  v-bind:class = "{
    completed: item.completed
  }"
  v-bind:key="item.id">
    <h2>{{item.title}}</h2>
    <button v-if="!item.completed" @click="markItem(item.id)"><img src="../public/correct.png" alt=""> Zrobione</button>
    <button class="remove" v-if="item.completed" @click="removeItem(item.id)"><img src="../public/trash.png" alt="">Usuń</button>
  </div>
</div>
</template>

<script>

export default {
  data() {
    return {
      newItem: '',
      items: [
        ],
    }
  },
  methods: {
    addItem() {
      this.items.push({title: this.newItem, completed: false, id: Math.random()})
      this.newItem = ''
    },
    markItem(id) {
      const index = this.items.findIndex(el => el.id === id)
      this.items[index].completed = "true"
    },

    removeItem(id) {
      const index = this.items.findIndex(el => el.id === id)
      this.items.splice(index, 1)
    }
  }
  
  }


</script>

<style>
#container {
  max-width: 800px;
  margin: auto;
  display: flex;
  place-items: center;
  justify-content: center;
  flex-direction: column;
}
button img {
  width: 15px;
}
.item {
  background: linear-gradient(20deg, rgb(135, 232, 0) 10%, white 90%);
  border: 2px solid rgb(135, 232, 0);
  border-radius: 10px;
  padding: 10px;
  margin-bottom: 10px;
  margin-top: 10px;
  width: 600px;
  text-align: center;
}



.completed h2 {
  text-decoration: line-through;
}

.remove {
  opacity: 1;
  color: red;
}
</style>