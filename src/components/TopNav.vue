<template>
  <div class="nav-wrapper">
    <!-- Top bar: logo + cart -->
    <nav class="top-bar">
      <div class="logo">
        <a href="/">
          <img src="/best-buy-logo.png" alt="Best Buy Logo">
        </a>
      </div>
      <button class="hamburger" @click="toggleNav">
        <span class="hamburger-icon"></span>
      </button>
      <ul class="nav-links" :class="{ 'nav-links--open': isNavOpen }">
        <li>
          <router-link to="/" @click="closeNav" class="nav-link-item">
            <svg viewBox="0 0 24 24" aria-hidden="true" class="nav-icon">
              <path d="M20 7h-7l-2-4H4C2.9 3 2 3.9 2 5v14c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V9c0-1.1-.9-2-2-2z"/>
            </svg>
            Products
          </router-link>
        </li>
        <li>
          <router-link to="/cart" @click="closeNav" class="nav-link-item">
            <svg viewBox="0 0 24 24" aria-hidden="true" class="nav-icon">
              <path d="M7 18c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2zm10 0c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2zM1 2v2h2l3.6 7.59-1.35 2.45C5.09 14.37 5 14.69 5 15c0 1.1.9 2 2 2h12v-2H7.42c-.14 0-.25-.11-.25-.25l.03-.12.9-1.63H19c.75 0 1.41-.41 1.75-1.03l3.58-6.49A1 1 0 0023 5H5.21L4.27 3H1z"/>
            </svg>
            Cart ({{ cartItemCount }})
          </router-link>
        </li>
      </ul>
    </nav>
    <!-- Category bar -->
    <div class="category-bar">
      <ul class="categories">
        <li
          v-for="cat in categories"
          :key="cat"
          :class="{ active: selectedCategory === cat }"
          @click="selectCategory(cat)"
        >
          {{ cat }}
          <svg class="chevron" focusable="false" viewBox="0 0 32 32" aria-hidden="true">
            <path d="M16,20.5a1,1,0,0,1-.74-.29l-7-6.91a1,1,0,0,1,0-1.48,1.06,1.06,0,0,1,1.49,0L16,17.92l6.18-6.13a1.06,1.06,0,0,1,1.49,0,1,1,0,0,1,0,1.48l-7,6.91A1,1,0,0,1,16,20.5Z"/>
          </svg>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TopNav',
  props: ['cartItemCount'],
  data() {
    return {
      isNavOpen: false,
      selectedCategory: 'All',
      categories: ['All', 'TVs', 'Computers', 'Phones', 'Headphones', 'Gaming', 'Tablets']
    }
  },
  methods: {
    toggleNav() {
      this.isNavOpen = !this.isNavOpen
    },
    closeNav() {
      this.isNavOpen = false
    },
    selectCategory(cat) {
      this.selectedCategory = cat
      this.$emit('filterCategory', cat)
    }
  }
}
</script>

<style scoped>
.nav-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
}

/* Top bar — Best Buy logo blue */
.top-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #0046BE;
  color: #fff;
  padding: 0.5rem 1rem 0.25rem 1rem;
}

nav img {
  width: 90px;
  height: auto;
}

.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 0.25rem;
}

.nav-link-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  color: #fff;
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 600;
  font-family: 'Arial', sans-serif;
  padding: 0.4rem 0.9rem;
  border-radius: 4px;
  transition: background-color 0.15s;
}

.nav-link-item:hover {
  background-color: rgba(255, 255, 255, 0.15);
}

.nav-icon {
  width: 28px;
  height: 28px;
  fill: #fff;
}

.hamburger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  margin: 0;
  margin-top: -40px;
}

.hamburger-icon {
  display: block;
  width: 20px;
  height: 2px;
  background-color: #fff;
  position: relative;
  top: 50%;
  transform: translateY(-50%);
}

.hamburger-icon::before,
.hamburger-icon::after {
  content: '';
  display: block;
  width: 20px;
  height: 2px;
  background-color: #fff;
  position: absolute;
  left: 0;
}

.hamburger-icon::before {
  top: -6px;
}

.hamburger-icon::after {
  bottom: -6px;
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background-color: #333;
    padding: 1rem;
  }

  .nav-links--open {
    display: block;
  }

  .nav-links--open li {
    padding: 0.5rem 0;
  }

  .hamburger {
    display: block;
  }
}

/* Category bar — darker Best Buy blue */
.category-bar {
  background-color: #003099;
  padding: 0;
}

.categories {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  justify-content: center;
}

.categories li {
  color: #fff;
  font-size: 0.95rem;
  font-weight: 700;
  font-family: 'Arial', sans-serif;
  letter-spacing: 0.01em;
  padding: 0.65rem 1.4rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 6px;
  border-bottom: 3px solid transparent;
  white-space: nowrap;
  transition: border-color 0.15s, background-color 0.15s;
}

.categories li:hover {
  background-color: rgba(255, 255, 255, 0.1);
  border-bottom: 3px solid #FFE000;
}

.categories li.active {
  border-bottom: 3px solid #FFE000;
}

.chevron {
  width: 18px;
  height: 18px;
  fill: #fff;
  flex-shrink: 0;
  position: relative;
  top: 1px;
}
</style>