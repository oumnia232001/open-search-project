<template>
    <div class="p-6 bg-gray-100 min-h-screen flex justify-center items-center">
      <div class="bg-white rounded-lg shadow-lg w-2/3">
        <!-- Header -->
        <div class="px-6 py-4 border-b border-gray-200 flex justify-between items-center">
          <h2 class="text-xl font-semibold">Product Table</h2>
          <input
            type="text"
            v-model="searchQuery"
            placeholder="Search for a product"
            class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-purple-500"
          />
        </div>
  
        <!-- Table -->
        <div class="overflow-x-auto">
          <table class="min-w-full table-auto">
            <thead class="bg-gray-100">
              <tr>
                <th class="px-6 py-3 text-left text-sm font-medium text-gray-500 uppercase tracking-wider">
                  Product Name
                </th>
                <th class="px-6 py-3 text-left text-sm font-medium text-gray-500 uppercase tracking-wider">
                  Price
                </th>
                <th class="px-6 py-3 text-left text-sm font-medium text-gray-500 uppercase tracking-wider">
                  Category
                </th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="product in filteredProducts"
                :key="product.id"
                class="border-b last:border-b-0 hover:bg-gray-50"
              >
                <td class="px-6 py-4 text-sm text-gray-700">{{ product.title }}</td>
                <td class="px-6 py-4 text-sm text-gray-700">${{ product.price }}</td>
                <td class="px-6 py-4 text-sm text-gray-700">{{ product.category }}</td>
              </tr>
            </tbody>
          </table>
        </div>
  
        <!-- Footer -->
        <div class="px-6 py-4 flex justify-end border-t border-gray-200">
          <button
            @click="discardChanges"
            class="px-4 py-2 mr-2 text-sm font-medium text-gray-500 border border-gray-300 rounded-lg hover:bg-gray-100"
          >
            Discard
          </button>
          <button
            @click="saveChanges"
            class="px-4 py-2 text-sm font-medium text-white bg-purple-500 rounded-lg hover:bg-purple-600"
          >
            Save
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref, computed, onMounted } from 'vue';
  import { fetchProducts } from '../services/api';
  
  export default defineComponent({
    name: 'ProductTable',
    setup() {
      const products = ref([]);
      const searchQuery = ref('');
  
      const filteredProducts = computed(() =>
        products.value.filter((product) =>
          product.title.toLowerCase().includes(searchQuery.value.toLowerCase())
        )
      );
  
      const discardChanges = () => {
        console.log('Changes discarded!');
      };
  
      const saveChanges = () => {
        console.log('Changes saved!');
      };
  
      onMounted(async () => {
        products.value = await fetchProducts();
      });
  
      return {
        products,
        searchQuery,
        filteredProducts,
        discardChanges,
        saveChanges,
      };
    },
  });
  </script>
  
  <style scoped>
  /* Ajoutez des styles personnalisés si nécessaire */
  </style>
