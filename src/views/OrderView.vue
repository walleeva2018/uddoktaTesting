<template>
  <div class="list-container">
    <h3>Orders</h3>
    <ul class="user-list">
      <li
        v-for="user in users"
        :key="user.id"
        :class="[getStatusClass(user), { 'is-marked': user.isMarked }]"
      >
        <div class="status">
          <i class="fa fa-circle"></i>
        </div>
        <div class="user-info">
          <span class="name">{{ user.name }}</span>
        </div>
        <div class="actions">
          <i class="fa fa-envelope" :class="{ disabled: user.status === 'offline' }"></i>
          <i class="fa fa-comment" :class="{ disabled: user.status === 'offline' }"></i>
          <button @click="markUser(user)">
            {{ user.isMarked ? 'Unmark' : 'Mark' }}
          </button>
          <button @click="deleteUser(user.id)">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const users = ref([
  { id: 1, name: 'Sherriff B.', status: 'active', isMarked: false },
  { id: 2, name: 'Waco K.', status: 'active', isMarked: false },
  { id: 3, name: 'Hedley L.', status: 'idle', isMarked: false },
  { id: 4, name: 'Lili V.S.', status: 'active', isMarked: false },
  { id: 5, name: 'William J.L.P.', status: 'offline', isMarked: false }
]);

const getStatusClass = (user) => {
  return {
    'is-active': user.status === 'active',
    'is-idle': user.status === 'idle',
    'is-offline': user.status === 'offline'
  };
};

const deleteUser = (id) => {
  users.value = users.value.filter((user) => user.id !== id);
};

const markUser = (user) => {
  user.isMarked = !user.isMarked;
};
</script>

<style scoped>
.list-container {
  width: 100%;

  margin: 0 auto;
  background: #033d54;
  padding: 1em;
  border-radius: 8px;
  color: white;
  font-family: Arial, sans-serif;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
}

h3 {
  margin-bottom: 1em;
  text-align: center;
  color: #40c4ff;
}

.user-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.user-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1em;
  background: #045370;
  border-radius: 6px;
  margin-bottom: 0.5em;
  transition: transform 0.2s;
}

.user-list li:hover {
  transform: translateY(-2px);
  background: #05658b;
}

.user-list li.is-marked {
  background: #1abc9c !important; /* Highlight marked items */
}

.user-list li:nth-child(odd) {
  background: #044d65;
}

.status i {
  font-size: 0.8em;
  margin-right: 0.5em;
}

.status i.fa-circle {
  color: #2ecc71; /* Default color (active) */
}

.user-list li.is-idle .status i.fa-circle {
  color: #f1c40f; /* Idle color */
}

.user-list li.is-offline .status i.fa-circle {
  color: #e74c3c; /* Offline color */
}

.user-info .name {
  font-weight: bold;
}

.actions i {
  margin-left: 0.5em;
  font-size: 1.2em;
  cursor: pointer;
  transition:
    color 0.2s,
    transform 0.2s;
}

.actions i:hover {
  color: #40c4ff;
  transform: scale(1.1);
}

.actions i.disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

.actions button {
  background: #3498db;
  color: white;
  border: none;
  padding: 0.5em 0.8em;
  margin-left: 0.5em;
  border-radius: 4px;
  font-size: 0.9em;
  cursor: pointer;
  transition:
    background 0.3s ease,
    transform 0.2s;
}

.actions button:hover {
  background: #1abc9c;
  transform: translateY(-1px);
}

.actions button:active {
  transform: scale(0.98);
}

@media (max-width: 600px) {
  .user-list li {
    flex-direction: column;
    align-items: flex-start;
  }

  .actions {
    margin-top: 0.5em;
  }
}
</style>
