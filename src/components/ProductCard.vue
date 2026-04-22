<template>
  <div class="product-card">
    <img :src="product.image" alt="Product Image">
    <router-link :to="`/product/${product.id}`">
      <h2>{{ product.name }}</h2>
    </router-link>
      <p>{{ product.description }}</p>
      <div class="product-details">
        <div class="product-price">
          <p class="price">${{ product.price.toFixed(2) }}</p>
        </div>
        <div class="product-controls">
          <input type="number" v-model="quantity" min="1" class="quantity-input" />
          <button @click="addToCart">Add to Cart</button>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: ['product'],
  data() {
    return {
      quantity: 1
    }
  },
  methods: {
    incrementQuantity() {
      this.quantity++
    },
    decrementQuantity() {
      if (this.quantity > 1) {
        this.quantity--
      }
    },
    addToCart() {
      // Add the product and quantity to the cart
      this.$emit('addToCart', {
        productId: this.product.id,
        quantity: this.quantity
      })
    }
  }
}
</script>

<style scoped>
.product-card {
  background: #fff;
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  padding: 1rem;
  transition: box-shadow 0.15s;
}

.product-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.12);
}

.product-card img {
  width: 100%;
  height: 180px;
  object-fit: contain;
  margin-bottom: 0.75rem;
  background: #f5f5f5;
  border-radius: 4px;
}

.product-card a {
  text-decoration: none;
  color: #1a1a1a;
}

.product-card h2 {
  font-size: 0.9rem;
  font-weight: 600;
  margin: 0 0 0.5rem 0;
  line-height: 1.3;
  min-height: 2.4em;
  color: #1a1a1a;
}

.product-card h2:hover {
  color: #0046BE;
}

.product-card p {
  font-size: 0.8rem;
  color: #555;
  line-height: 1.4;
  margin: 0 0 0.75rem 0;
  flex-grow: 1;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.product-details {
  margin-top: auto;
}

.price {
  font-size: 1.3rem;
  font-weight: 700;
  color: #1a1a1a;
  margin: 0 0 0.6rem 0;
}

.product-controls {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.quantity-input {
  width: 52px;
  padding: 6px 4px;
  border: 1px solid #ccc;
  border-radius: 4px;
  text-align: center;
  font-size: 0.9rem;
}

button {
  flex: 1;
  background-color: #0046BE;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 8px 12px;
  font-size: 0.85rem;
  font-weight: 700;
  cursor: pointer;
  transition: background-color 0.15s;
}

button:hover {
  background-color: #003099;
}
</style>