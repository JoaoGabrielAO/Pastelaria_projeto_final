<template>
  <div id="main-banner">
    <h1>Pastéis quentinhos e crocantes 🥟</h1>
  </div>
</template>
<script>
export default {
  name: "BannerComponent",
};
</script>
<style scoped>
#main-banner {
  background-image: linear-gradient(135deg, #b5451b 0%, #7a2d10 60%, #3d1508 100%);
  height: 300px;
  background-position: 0;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

#main-banner h1 {
  font-size: 40px;
  color: antiquewhite;
  background: #7a2d10;
  padding: 25px;
  border-radius: 100px 0px 0px 100px;
}
</style>