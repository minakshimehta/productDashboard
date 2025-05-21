<template>
  <form class="product-form-inline" @submit.prevent="submitForm">
    <input
      v-model="form.title"
      placeholder="Product Title"
      required
      class="input-field"
    />

    <input
      v-model.number="form.price"
      type="number"
      placeholder="Price"
      required
      class="input-field"
    />

    <input
      v-model="form.image"
      type="url"
      placeholder="Image URL"
      required
      class="input-field"
    />

    <button class="submit-btn" type="submit">
      {{ isEdit ? 'Update' : 'Add' }}
    </button>
  </form>
</template>



<script setup>
import { reactive, watchEffect } from 'vue';

const props = defineProps(['product']);
const emit = defineEmits(['submit']);

const form = reactive({ title: '', price: '', image: '' });
const isEdit = props.product !== null;

watchEffect(() => {
  if (props.product) {
    form.title = props.product.title;
    form.price = props.product.price;
    form.image = props.product.image || '';
  } else {
    form.title = '';
    form.price = '';
    form.image = '';
  }
});


function submitForm() {
  emit('submit', { ...form });

  form.title = '';
  form.price = '';
  form.image = '';
}




</script>

<style scoped>
.product-form-inline {
  display: flex;
  gap: 1rem;
  align-items: center;
  padding: 1rem;
  background: #ffffff;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
  flex-wrap: wrap;
  max-width: 100%;
}

.input-field {
  padding: 0.6rem 1rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
  flex: 1 1 200px;
  transition: border-color 0.2s;
}

.input-field:focus {
  border-color: #2196f3;
  outline: none;
}

.submit-btn {
  padding: 0.6rem 1.2rem;
  background-color: #2196f3;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.submit-btn:hover {
  background-color: #1976d2;
}

</style>

