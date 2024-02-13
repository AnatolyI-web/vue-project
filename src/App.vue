<template>
  <main>
    <div class="menu">
      <div>
        <h1>Nova Polozka</h1>
      </div>
      <div>
        <h2>Nazov polozky</h2>
        <input v-model="input" placeholder="Maslo">
        <button @click="addItem()">Pridat</button>
      </div>
      <div>
        <h2>Polozky</h2>
        <ul>
          <li v-for="item in validItems" :key="`item-${item.id}`">
            <span @click="deleteItem(item)" style="margin-right: 15px">X</span>
            {{ item.text }}
          </li>
        </ul>
      </div>
      <h2>Vymazane polozky</h2>
        <ul>
          <li v-for="item in deletedItems" :key="`item-${item.id}`" className="vymazane-polozky">
            {{ item.text }}
          </li>
        </ul>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      input: '',
      list: [],
    }
  },
  computed: {
    validItems() {
      return this.list.filter(item => !item.is_deleted);
    },
    deletedItems() {
      return this.list.filter(item => item.is_deleted);
    }
  },
  methods: {
    addItem() {
      this.list.push({
        id: this.list.length + 1,
        text: this.input,
        is_deleted: false
      });
      this.input = '';
    },
    deleteItem(item) {
      item.is_deleted = true;
    },
  },
}
</script>

<style>
body{
  background: #333;
  color: #e0e0e0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
.menu{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
main{
  width: 100%;
  height: 100%;
}
input{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  margin-bottom: 1rem;;
}
.vymazane-polozky{
  text-decoration: line-through;
}
</style>
