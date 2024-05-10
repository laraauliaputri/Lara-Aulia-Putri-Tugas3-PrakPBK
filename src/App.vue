<template>
  <div id="app">
    <div class="header">
      <h1 class="title">Selamat datang, Swifties! 🎵</h1>
      <h2 class="subtitle">Ini To-Do List untuk Album Taylor Swiftmu! ✨</h2>
      <form @submit.prevent="addItem">
        <div class="form-group">
          <input type="text" v-model="newItem.name" placeholder="Tambahkan album baru">
          <input type="date" v-model="newItem.deadline" placeholder="Tenggat waktu">
          <button type="submit">Tambah</button>
        </div>
      </form>
      <p v-if="albums.length === 0" class="empty-msg">Belum ada album yang ditambahkan. Yuk tambah sekarang juga!</p>
      <ul v-if="albums.length > 0" class="album-list">
        <li v-for="(album, index) in albums" :key="index">
          <span :class="{ 'done': album.done }">{{ album.name }}</span>
          <span class="deadline">{{ album.deadline }}</span>
          <button @click="editItem(index)">Edit</button>
          <button @click="toggleDone(index)">{{ album.done ? 'Batal' : 'Selesai' }}</button>
          <button @click="deleteItem(index)">Hapus</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newItem: { name: '', deadline: '' },
      albums: []
    };
  },
  methods: {
    addItem() {
      if (this.newItem.name.trim() !== '') {
        this.albums.push({ name: this.newItem.name, done: false, deadline: this.newItem.deadline });
        this.newItem = { name: '', deadline: '' };
      }
    },
    deleteItem(index) {
      this.albums.splice(index, 1);
    },
    editItem(index) {
      const newValue = prompt('Edit item:', this.albums[index].name);
      if (newValue !== null && newValue.trim() !== '') {
        this.albums[index].name = newValue;
      }
    },
    toggleDone(index) {
      this.albums[index].done = !this.albums[index].done;
    }
  }
}
</script>

<style>
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background-color: #ffe7e7; /* Warna abu-abu muda */
}

.header {
  text-align: center;
  margin-bottom: 20px;
}

.title {
  font-size: 32px; /* Ukuran font yang lebih besar */
  font-weight: bold;
  color: #ff66cc; /* Warna pink */
  font-family: 'Playfair Display', serif; /* Gaya font Playfair Display */
}

.subtitle {
  font-size: 18px; /* Ukuran font yang lebih kecil */
  color: #ff66cc; /* Warna pink */
  font-family: 'Playfair Display', serif; /* Gaya font Playfair Display */
}


.empty-msg {
  text-align: center;
  margin-top: 10px;
}

.form-group {
  display: flex;
  align-items: center;
}

form {
  margin-bottom: 20px;
}

input {
  padding: 8px;
  margin-right: 10px;
}

input[type="date"] {
  padding: 6px;
}

button[type="submit"] {
  padding: 8px 15px;
  background-color: #ef93be;
  color: #0d1113;
  border: none;
  cursor: pointer;
}

button[type="submit"]:hover {
  background-color: #6b8f9c;
}

.album-list {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 0;
  border-bottom: 1px solid #ccc;
}

span {
  flex: 1;
}

.done {
  text-decoration: line-through;
  color: #999;
}

.deadline {
  flex: 1;
  text-align: right;
  margin-right: 20px;
}
</style>