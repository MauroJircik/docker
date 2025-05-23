
<template>
  <div>
    <h2>Usuários</h2>
    <ul>
      <li v-for="u in users" :key="u.id">{{ u.name }} ({{ u.email }})</li>
    </ul>
    <h2>Compras</h2>
    <ul>
      <li v-for="p in purchases" :key="p.id">
        {{ p.user?.name }} comprou {{ p.quantity }}x {{ p.item?.name }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const users = ref([])
const purchases = ref([])

onMounted(async () => {
  users.value = (await axios.get('http://backend:3001/users')).data
  purchases.value = (await axios.get('http://backend:3001/purchases')).data
})
</script>
