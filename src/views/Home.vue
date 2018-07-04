<template>
  <div>
    <Navbar/>
    <Content/>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Content from '@/components/Content.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    Content
  }
}
</script>
