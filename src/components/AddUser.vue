<template>
  <div>
    <h3>Добавить Пользователя</h3>
    <form @submit.prevent="handleSubmit">
      <div>
        <label for="name">Имя:</label>
        <input v-model="name" id="name" required />
      </div>
      <div>
        <label for="email">Email:</label>
        <input v-model="email" id="email" type="email" required />
      </div>
      <button type="submit">Добавить</button>
    </form>
    <div v-if="isLoading">Добавление пользователя...</div>
    <div v-if="isError">Ошибка: {{ error.message }}</div>
  </div>
</template>

<script setup>
import { useMutation, useQueryClient } from '@tanstack/vue-query';
import axios from 'axios';
import { ref } from 'vue';

const name = ref('');
const email = ref('');

const queryClient = useQueryClient();

// Функция для добавления пользователя
const addUser = async newUser => {
  const res = await axios.post(
    'https://jsonplaceholder.typicode.com/users',
    newUser
  );
  console.log(res.data);
  return res.data;
};

// Использование хука useMutation с обновлением кэша вручную
const mutation = useMutation({
  mutationFn: addUser,
  onSuccess: newUser => {
    // Получаем текущий список пользователей из кэша
    const existingUsers = queryClient.getQueryData(['users']);
    // Добавляем нового пользователя в список
    if (existingUsers) {
      queryClient.setQueryData(['users'], [...existingUsers, newUser]);
    }
  }
});

const { isLoading, isError, error, mutate } = mutation;

// Обработчик отправки формы
const handleSubmit = () => {
  mutate({
    name: name.value,
    email: email.value
  });
  // Очистить форму
  name.value = '';
  email.value = '';
};
</script>

<style scoped>
form {
  margin-top: 20px;
  padding: 10px;
  border: 1px solid #ccc;
  max-width: 400px;
}
form div {
  margin-bottom: 10px;
}
label {
  display: inline-block;
  width: 50px;
}
input {
  padding: 5px;
  width: 300px;
}
button {
  padding: 5px 10px;
}
</style>
