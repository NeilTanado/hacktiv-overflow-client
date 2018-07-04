<template>
  <div>
    <Navbar/>
    <h1>Training Website using Vue and Bootstrap</h1>
    <h1> Created By Neil Tanado </h1>
    <h1>Hacktiv8</h1>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'home',
  components: {
    Navbar
  }
}
</script>
