<template>
  <div class="home">
    <h1>Zlecenia lekowe</h1>
    <router-link class="btn" to="/order">Kreator zleceń</router-link>
    <router-link class="btn" to="/contact">Kontakt</router-link>
  </div>
</template>

<style lang="scss">
.home {
  background-image: url(../assets/1592309771_tmp_1282794.jpg);
  background-position: center;
  background-size: cover;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 0 20px;
}

.home h1 {
  font-size: 50px;
  text-transform: uppercase;
}

@media (max-width: 530px) {
  .home h1 {
    font-size: 40px;
  }
}

@media (max-width: 430px) {
  .home h1 {
    font-size: 25px;
  }
}

.home .btn {
  font-size: 12px;
  text-decoration: none;
  color: #485e74;
  border: 1px solid #485e74;
  padding: 10px 20px;
  border-radius: 10px;
  margin-top: 10px;
}

.home .btn:hover {
  color: white;
  background-color: #485e74;
}
</style>
