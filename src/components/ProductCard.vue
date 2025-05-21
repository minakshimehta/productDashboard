<template>
    <div class="card">
      <img :src="product.image" alt="Product Image" class="product-image" />
      <div class="card-content">
        <h3 class="title">{{ product.title }}</h3>
        <p class="price">₹{{ product.price }}</p>
        <!-- <img :src="product.image" alt="Product Image" class="product-image" /> -->

        <div class="card-actions">
          <button class="btn edit" @click="$emit('edit', product)">Edit</button>
          <button class="btn delete" @click="$emit('delete', product.id)">Delete</button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps(['product'])
  </script>
  
  <style scoped>
  .card {
    display: flex;
    border: 1px solid #e0e0e0;
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
    overflow: hidden;
    margin-bottom: 1rem;
    transition: transform 0.2s ease;
    background-color: #fff;
  }
  
  .card:hover {
    transform: scale(1.01);
  }
  
  .product-image {
    width: 120px;
    height: 120px;
    object-fit: contain;
    background: #f9f9f9;
    padding: 10px;
  }
  
  .card-content {
    flex: 1;
    padding: 1rem;
  }
  
  .title {
    font-size: 1rem;
    font-weight: 600;
    margin: 0 0 0.5rem;
  }
  
  .price {
    font-size: 1.1rem;
    color: #2b9348;
    margin-bottom: 0.75rem;
  }
  
  .card-actions {
    display: flex;
    gap: 10px;
  }
  
  .btn {
    padding: 0.4rem 0.8rem;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.9rem;
  }
  
  .edit {
    background-color: #2196f3;
    color: white;
  }
  
  .edit:hover {
    background-color: #1976d2;
  }
  
  .delete {
    background-color: #f44336;
    color: white;
  }
  
  .delete:hover {
    background-color: #d32f2f;
  }
  </style>
  