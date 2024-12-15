<template>
  <div>
    <h2>Список Пользователей</h2>
    <AddUser />
    <div v-if="isLoading">Загрузка...</div>
    <div v-else-if="isError">Ошибка: {{ error.message }}</div>
    <ul v-else>
      <li v-for="user in data" :key="user.id">
        {{ user.name }} - {{ user.email }}
      </li>
    </ul>
    <button @click="refetch">Обновить</button>
  </div>
</template>

<script setup>
import { useQuery } from '@tanstack/vue-query';
import axios from 'axios';
import AddUser from './AddUser.vue';

// Функция для загрузки пользователей
const fetchUsers = async () => {
  const res = await axios.get('https://jsonplaceholder.typicode.com/users');
  return res.data;
};

// Использование хука useQuery для получения данных
const { data, error, isLoading, isError, refetch } = useQuery({
  queryKey: ['users'],
  queryFn: fetchUsers
});
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  padding: 5px 0;
}
button {
  margin-top: 10px;
  padding: 5px 10px;
}
</style>
