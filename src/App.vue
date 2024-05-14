<template>
  <div id="app" class="container">
    <h1 class="header">App To Do List</h1>
    <div class="input-container">
      <input type="text" v-model="newTask" placeholder="Tambahkan tugas baru" />
      <button @click="addTask">Tambah</button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task">
        <span>{{ task }}</span>
        <div class="actions">
          <button @click="editTask(index)" class="edit">Edit</button>
          <button @click="deleteTask(index)">Hapus</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      newTask: "",
      tasks: ["Tugas3 CRUD(Contoh)"],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push(this.newTask.trim());
        this.newTask = "";
      }
    },
    editTask(index) {
      const taskToEdit = this.tasks[index];

      const updatedTask = prompt("Edit tugas:", taskToEdit);

      if (updatedTask !== null) {
        const trimmedTask = updatedTask.trim();

        if (trimmedTask !== "") {
          this.tasks.splice(index, 1, trimmedTask);
        } else {
          alert("Teks yang dimasukkan tidak boleh kosong.");
        }
      } else {
        alert("Edit tugas dibatalkan.");
      }
    },
    deleteTask(index) {
      if (confirm("Anda yakin ingin menghapus tugas ini?")) {
        this.tasks.splice(index, 1);
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Segoe UI", sans-serif;
  background-color: #f8f8f8;
  color: #333;
  line-height: 1.6;
}

.container {
  max-width: 800px;
  margin: 100px;
  border-radius: 10px;
  background: rgba(16, 140, 255, 0.467);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(8px);
}

.header {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 20px;
}

.input-container {
  display: flex;
  margin-bottom: 20px;
}

.input-container input[type="text"] {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.input-container button {
  margin-left: 10px;
  padding: 10px 20px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.input-container button:hover {
  background-color: #45a049;
}

ul {
  list-style-type: none;
}

.task {
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #f9f9f9;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.task .actions button {
  padding: 5px 10px;
  background-color: #f44336;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.task .actions button.edit {
  background-color: #2196f3;
}

.task .actions button:hover {
  background-color: #d32f2f;
}

.task .actions button.edit:hover {
  background-color: #1976d2;
}
</style>
