<template>
  <div>
    <Navbar/>
    <ContentQuestion/>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import ContentQuestion from '@/components/ContentQuestion.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    ContentQuestion
  }
}
</script>
