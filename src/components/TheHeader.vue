<template>
  <div class="header"> Форма создания клиента </div>
</template>

<script>
  export default {
    name: "TheHeader"
  }
</script>

<style scoped>
.header{
  display: flex;
  position: fixed;
  top: 0;
  text-align: center;
  justify-content: center;
  align-content: center;
  vertical-align: middle;
  height: 3vw;
  min-height: fit-content;
  line-height: 3vw;
  background: #43799b;
  color: white;
  padding: 5px;
  width: 100vw;
  font-size: 20px;
  z-index: 100;
}
</style>