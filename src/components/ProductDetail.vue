<template>
  <div class="detail-wrapper">
    <div class="breadcrumb" v-if="productExists">
      <router-link to="/">← Back to Products</router-link>
    </div>

    <div class="product-detail" v-if="productExists">
      <div class="product-image">
        <img :src="product.image" :alt="product.name" />
      </div>

      <div class="product-info">
        <p class="brand">{{ brand }}</p>
        <h1>{{ product.name }}</h1>
        <p class="description">{{ product.description }}</p>

        <div class="price-row">
          <span class="price">${{ product.price.toFixed(2) }}</span>
          <span class="in-stock">✓ In Stock</span>
        </div>

        <div class="add-to-cart">
          <input type="number" v-model="quantity" min="1" class="quantity-input" />
          <button @click="addToCart">Add to Cart</button>
        </div>
      </div>
    </div>

    <div class="not-found" v-else>
      <img src="../assets/404.jpg" alt="Product not found" />
      <h3>Oops! That product was not found.</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductDetail',
  props: ['products'],
  data() {
    return {
      quantity: 1
    }
  },
  computed: {
    product() {
      return this.products.find(product => product.id == this.$route.params.id);
    },
    productExists() {
      return !!this.product;
    },
    brand() {
      return this.product?.name.split(' ')[0] ?? '';
    }
  },
  methods: {
    addToCart() {
      this.$emit('addToCart', {
        productId: this.product.id,
        quantity: this.quantity
      })
    }
  }
}
</script>

<style scoped>
.detail-wrapper {
  max-width: 1100px;
  margin: 0 auto;
  padding: 1.5rem 2rem;
}

.breadcrumb {
  margin-bottom: 1.25rem;
  font-size: 0.9rem;
}

.breadcrumb a {
  color: #0046BE;
  text-decoration: none;
  font-weight: 600;
}

.breadcrumb a:hover {
  text-decoration: underline;
}

.product-detail {
  display: flex;
  align-items: flex-start;
  gap: 3rem;
}

.product-image {
  flex: 0 0 52%;
  background: #f5f5f5;
  border-radius: 8px;
  padding: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.product-image img {
  width: 100%;
  max-height: 420px;
  object-fit: contain;
}

.product-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.brand {
  font-size: 0.85rem;
  font-weight: 700;
  color: #0046BE;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin: 0;
}

.product-info h1 {
  font-size: 1.75rem;
  font-weight: 700;
  color: #1a1a1a;
  line-height: 1.2;
  margin: 0;
}

.description {
  font-size: 0.95rem;
  color: #444;
  line-height: 1.6;
  margin: 0;
}

.price-row {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-top: 0.5rem;
}

.price {
  font-size: 2rem;
  font-weight: 700;
  color: #1a1a1a;
}

.in-stock {
  font-size: 0.9rem;
  font-weight: 600;
  color: #2e7d32;
}

.add-to-cart {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-top: 0.5rem;
}

.quantity-input {
  width: 60px;
  padding: 10px 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  text-align: center;
  font-size: 1rem;
}

button {
  flex: 1;
  background-color: #0046BE;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 12px 24px;
  font-size: 1rem;
  font-weight: 700;
  cursor: pointer;
  transition: background-color 0.15s;
}

button:hover {
  background-color: #003099;
}

.not-found {
  text-align: center;
  padding: 3rem;
}

@media (max-width: 768px) {
  .product-detail {
    flex-direction: column;
  }

  .product-image {
    flex: none;
    width: 100%;
  }
}
</style>