<template>
  <div class="min-h-screen bg-gray-100">
    <h1 class="text-2xl font-bold text-center p-4">Liste des Produits</h1>
    <ProductTable />
  </div>
</template>

<script lang="ts">
import ProductTable from './components/ProductTable.vue';

export default {
  name: 'App',
  components: {
    ProductTable,
  },
};
</script>