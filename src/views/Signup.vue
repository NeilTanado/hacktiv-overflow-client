<template>
  <div>
    <Navbar/>
    <Register/>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Register from '@/components/Register.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    Register
  }
}
</script>
