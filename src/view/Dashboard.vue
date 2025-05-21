<template>
  <h2 class="dashboard-title">Product Dashboard</h2>
  <div class="search-wrapper">
    <input v-model="search"       placeholder="🔍 Search products..."
    class="search-input"
/>

  </div>

  <ProductForm :product="editing" @submit="handleForm" />

  <ProductCard
    v-for="p in filtered"
    :key="p.id"
    :product="p"
    @edit="editing = $event"
    @delete="remove"
  />
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import { getProducts, addProduct, updateProduct, deleteProduct } from '../services/api';
import ProductCard from '../components/ProductCard.vue';
import ProductForm from '../components/ProductForm.vue';

const products = ref([]);
const editing = ref(null);
const search = ref('');

onMounted(async () => {
  const res = await getProducts();
  products.value = res.data;
});

const filtered = computed(() =>
  products.value.filter(p =>
    p.title.toLowerCase().includes(search.value.toLowerCase())
  )
);

async function handleForm(data) {
  if (editing.value) {
    const res = await updateProduct(editing.value.id, data);
    const idx = products.value.findIndex(p => p.id === editing.value.id);
    products.value[idx] = res.data;
    editing.value = null;
  } else {
    const res = await addProduct(data);
    products.value.push({ ...data, id: Date.now() }); 
  }
}

async function remove(id) {
  await deleteProduct(id);
  products.value = products.value.filter(p => p.id !== id);
}
</script>

<style scoped>
.dashboard-title{

  text-align: center;

  font-size: 2.5rem;
}
.search-wrapper {
  display: flex;
  justify-content: center;
  margin: 20px 0;
}

.search-input {
  min-width: 300px;
  padding: 12px 20px;
  border: none;
  border-radius: 25px;
  background-color: #f1f3f5;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
  font-size: 1rem;
  outline: none;
  transition: all 0.2s ease-in-out;
}

.search-input::placeholder {
  color: #888;
}

.search-input:focus {
  background-color: #ffffff;
  box-shadow: 0 0 0 3px rgba(33, 150, 243, 0.2);
}

</style>