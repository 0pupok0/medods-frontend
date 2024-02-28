<template>
<div class="page">
  <the-header></the-header>
  <user-create-form class="content"></user-create-form>
</div>
</template>

<script>
import TheHeader from './components/TheHeader.vue'
import UserCreateForm from "@/components/UserCreateForm.vue";

export default {
  name: 'App',
  components: {
    UserCreateForm,
    TheHeader
  }
}
</script>

<style>
@font-face {
  font-family: 'Rateway';
  src: url('@/assets/Raleway-VariableFont_wght.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;
}
.page{
  font-family: Rateway,serif;
  background-image: url("assets/background.jpg");
  background-size: 100%;
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  background-color: #2e2e39;
  padding-bottom: 5vw;
  margin-top: 3vw;
}

.content{
  margin-top: 10vw;
  padding-top: 5vw;
  border-radius: 30px;
}
</style>
