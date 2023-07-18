<template>
  <div id="app">
    <router-view />
  </div>
</template>


<style lang="scss">
@import "bootstrap/dist/css/bootstrap.css";
#app {
  font-family: "Poppins", sans-serif;

}
.custom-container {
  max-width: fit-content;
  margin: 0 auto;
  display: flex;
}
@media screen and (min-width: 320px) and (max-width: 767px) {
}

@media screen and (min-width: 768px) {
}
@media screen and (min-width: 1200px) {
  .custom-container {
    max-width: fit-content;
    margin: 0 auto;
    display: flex;
  }
}
</style>
