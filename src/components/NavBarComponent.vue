<template>
  <div>
    <nav id="nav">
      <router-link to="/" id="logo-url">
        <span id="logo">🥟 Pastelaria do João</span>
      </router-link>
      <router-link to="/">Home</router-link> |
      <router-link to="/menu">Menu</router-link> |
      <router-link to="/pedidos">Pedidos</router-link>
    </nav>
  </div>
</template>
<script>
export default {
  name: "NavBarComponent",
};
</script>
<style scoped>
#logo {
  font-size: 22px;
  font-weight: bold;
  color: #f0a500;
}

#logo:hover {
  color: #fff;
  transition: 0.2s;
}

#nav #logo-url {
  margin: auto;
  margin-left: 0;
  text-decoration: none;
}

#nav {
  background-color: #7a2d10;
  border-bottom: #f0a500 4px solid;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

#nav a {
  color: #f0a500;
  text-decoration: none;
  margin-left: 20px;
  font-size: 18px;
}

#nav a:hover {
  color: white;
  font-size: 22px;
  transition: 0.2s;
}
</style>