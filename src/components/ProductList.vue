<template>
  <div>
    <div class="hero">
      <h1 class="hero-title">Top Tech. Unbeatable Prices.</h1>
      <p class="hero-subtitle">Explore our wide selection of electronics, from TVs to laptops and everything in between.</p>
      <button class="shop-all-btn" @click="scrollToProducts">Shop All</button>
    </div>
    <div class="product-list" ref="productGrid">
      <ProductCard
          v-for="product in products"
          :key="product.id"
          :product="product"
          @addToCart="addToCart"
        />
    </div>
  </div>
</template>

<script>
  import ProductCard from '../components/ProductCard'

  export default {
    name: 'ProductList',
    props: ['products'],
    components: {
      ProductCard
    },
    methods: {
      addToCart({ productId, quantity }) {
        this.$emit('addToCart', {
          productId: productId,
          quantity: quantity
        })
      },
      scrollToProducts() {
        this.$refs.productGrid.scrollIntoView({ behavior: 'smooth' })
      }
    }
  }
</script>

<style scoped>
.hero {
  background: linear-gradient(135deg, #e8f0fe 0%, #c7d9f8 100%);
  text-align: center;
  padding: 3rem 2rem;
  margin-bottom: 1.5rem;
}

.hero-title {
  font-size: 2.2rem;
  font-weight: 800;
  color: #003099;
  margin-bottom: 0.75rem;
}

.hero-subtitle {
  font-size: 1.1rem;
  color: #333;
  margin-bottom: 1.5rem;
}

.shop-all-btn {
  background-color: #0046BE;
  color: #fff;
  font-size: 1rem;
  font-weight: 700;
  padding: 0.75rem 2rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.15s;
}

.shop-all-btn:hover {
  background-color: #003099;
}

.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 1.25rem;
  max-width: 1400px;
  margin: 0 auto 3rem auto;
  padding: 0 2rem;
}
</style>