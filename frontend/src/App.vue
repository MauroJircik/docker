<template>
  <div>
    <h1>Meu App de Papelaria</h1>

    <section>
      <h2>Usuários</h2>
      <ul>
        <li v-for="usuario in usuarios" :key="usuario.id">
          {{ usuario.nome }}
        </li>
      </ul>
    </section>

    <section>
      <h2>Itens de Papelaria</h2>
      <ul>
        <li v-for="item in itens" :key="item.id">
          {{ item.nome }} - R$ {{ item.preco.toFixed(2) }}
        </li>
      </ul>
    </section>

    <section>
      <h2>Compras</h2>
      <ul>
        <li v-for="compra in compras" :key="compra.id">
          Compra de {{ compra.quantidade }}x do item #{{ compra.ItemId }}
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      usuarios: [],
      itens: [],
      compras: [],
    };
  },
  async mounted() {
    try {
      const [usuariosRes, itensRes, comprasRes] = await Promise.all([
        axios.get('http://localhost:3000/usuarios'),
        axios.get('http://localhost:3000/itens'),
        axios.get('http://localhost:3000/compras'),
      ]);
      this.usuarios = usuariosRes.data;
      this.itens = itensRes.data;
      this.compras = comprasRes.data;
    } catch (error) {
      console.error('Erro ao carregar dados:', error);
    }
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 20px;
}
h1 {
  color: #2c3e50;
}
section {
  margin-top: 30px;
}
</style>

