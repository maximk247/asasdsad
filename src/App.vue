<template>
  <div id="app">
    <h1>Мониторинг Продаж</h1>
    <SalesChart />
    <UsersList />
  </div>
</template>

<script setup>
import SalesChart from './components/SalesChart.vue';
import UsersList from './components/UsersList.vue';
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 20px;
}
h1 {
  text-align: center;
  margin-bottom: 40px;
}
</style>
