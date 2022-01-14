<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Crypto Wallet</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link :active-class="'active'" class="nav-link" to="/">Dashboard</router-link>
            </li>
            <li class="nav-item">
              <router-link :active-class="'active'" class="nav-link" to="/about">Wallets</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
<!--    <div id="nav">
      <router-link to="/">Dashboard</router-link> |
      <router-link to="/about">Wallets</router-link>
    </div>-->
    <router-view/>
  </div>
</template>

<style>
/*
Bootstrap v5 import
*/
@import "https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css";
</style>
