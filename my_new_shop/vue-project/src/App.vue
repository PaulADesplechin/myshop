<template>
  <div id="app">
    <header>
      <nav>
        <router-link to="/">Accueil</router-link>
        <router-link to="/products">Produits</router-link>
      </nav>
    </header>
    <router-view />
  </div>
</template>

<style>
nav {
  display: flex;
  justify-content: space-around;
  background-color: #007bff;
  padding: 10px;
}
nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}
</style>
