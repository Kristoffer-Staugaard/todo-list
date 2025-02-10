<script setup>
import { ref } from "vue";

const NewAssignment = ref("");
const assignment = ref([]);

const addAssignment = () => {
  assignment.value.push({
    text: NewAssignment.value,
    isEditable: false,
  });
  NewAssignment.value = "";
};

const deleteAssignment = (index) => {
  assignment.value.splice(index, 1);
};
</script>

<template>
  <div class="todo-container">
    <div class="todo-input-group">
      <input v-model="NewAssignment" />
      <button @click="addAssignment" class="btn btn-primary">Ny opgave</button>
    </div>
    <div class="todo-list">
      <div v-for="(item, index) in assignment" :key="index" class="todo-item">
        <p v-bind:contenteditable="item.isEditable" class="todo-text">
          {{ item.text }}
        </p>
        <button @click="item.isEditable = !item.isEditable" class="btn btn-edit">
          {{ item.isEditable ? "Gem" : "Rediger" }}
        </button>
        <button @click="deleteAssignment(index)" class="btn btn-delete">Slet</button>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

.todo-container {
  max-width: 800px;
  height: 100%;
  margin: 0 auto;
  padding: 16px;
  background-color: #F7F4EE;
}

.todo-input-group {
  margin-bottom: 24px;
  display: flex;
  gap: 8px;

  input {
    flex: 1;
    padding: 8px 12px;
    border: 1px solid #ECE4D5;
    border-radius: 4px;
    font-size: 16px;
    background-color: #fff;

    &:focus {
      outline: 2px solid #EE6C4D;
    }
  }
}

.todo-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 12px;
  background-color: #fff;
  border-radius: 4px;
  gap: 8px;
  border: 1px solid #ECE4D5;
}

.todo-text {
  flex-grow: 1;
  margin: 0;
  padding: 4px 8px;
  min-height: 24px;

  &[contenteditable="true"] {
    background-color: #fff;
    border: 1px solid #ECE4D5;
    border-radius: 4px;
    padding: 4px 8px;
  }
}

.btn {
  padding: 8px 16px;
  border: none;
  border-radius: 16px;
  color: white;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s ease;

  &:hover {
    transform: translateY(-1px);
  }
}

.btn-primary {
  background-color: #EE6C4D;
}

.btn-edit {
  background-color: #3D5A80;
}

.btn-delete {
  background-color: #98C1D9;
  &:hover {
    background-color: #EE6C4D;
  }
}
</style>
