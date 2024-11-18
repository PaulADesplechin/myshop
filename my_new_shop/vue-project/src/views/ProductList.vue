<template>
  <main>
    <header>
      <h1>Bienvenue sur MyGolfShop</h1>
      <p>Découvrez nos produits de golf premium !</p>
    </header>

    <!-- Filtres -->
    <section class="filters">
      <label>
        Filtrer par prix :
        <select v-model="priceFilter" @change="applyFilter">
          <option value="all">Tous</option>
          <option value="low">Moins de 200€</option>
          <option value="high">Plus de 200€</option>
        </select>
      </label>
    </section>

    <!-- Liste des produits -->
    <section class="products">
      <div
        v-for="product in filteredProducts"
        :key="product.id"
        class="product-card"
      >
        <img :src="product.image" :alt="product.name" class="product-image" />
        <h2>{{ product.name }}</h2>
        <p>{{ product.price }} €</p>
        <button @click="addToCart(product)">Ajouter au panier</button>
      </div>
    </section>

    <!-- Panier -->
    <section class="cart" v-if="cart.length > 0">
      <h2>Votre Panier</h2>
      <ul>
        <li v-for="item in cart" :key="item.id">
          {{ item.name }} - {{ item.price }} €
          <button @click="removeFromCart(item)">Retirer</button>
        </li>
      </ul>
      <p>Total : {{ cartTotal }} €</p>
    </section>
  </main>
</template>

<script>
export default {
  name: "ProductList",
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Callaway Rogue",
          price: 399,
          image: "/src/assets/image/callaway-rogue.jpeg",
        },
        {
          id: 2,
          name: "TaylorMade M4",
          price: 499,
          image: "/src/assets/image/taylormade-m4.jpeg",
        },
        {
          id: 3,
          name: "Wilson Harmonized",
          price: 99,
          image: "/src/assets/image/wilson-harmonized.jpeg",
        },
      ],
      cart: [],
      priceFilter: "all",
      filteredProducts: [],
    };
  },
  computed: {
    cartTotal() {
      return this.cart.reduce((total, item) => total + item.price, 0);
    },
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    removeFromCart(item) {
      this.cart = this.cart.filter((product) => product.id !== item.id);
    },
    applyFilter() {
      if (this.priceFilter === "low") {
        this.filteredProducts = this.products.filter((p) => p.price < 200);
      } else if (this.priceFilter === "high") {
        this.filteredProducts = this.products.filter((p) => p.price >= 200);
      } else {
        this.filteredProducts = this.products;
      }
    },
  },
  mounted() {
    this.filteredProducts = this.products;
  },
};
</script>

<style scoped>
main {
  max-width: 1200px;
  margin: auto;
  padding: 20px;
}

header {
  text-align: center;
  margin-bottom: 20px;
}

.filters {
  margin-bottom: 20px;
  text-align: center;
}

.products {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}

.product-card {
  border: 1px solid #ddd;
  text-align: center;
  padding: 10px;
  border-radius: 10px;
}

.product-image {
  width: 100%;
  height: auto;
  border-radius: 5px;
}

button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.cart {
  margin-top: 20px;
  text-align: center;
}
</style>
