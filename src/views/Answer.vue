<template>
  <div>
    <Navbar/>
    <ContentAnswer/>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import ContentAnswer from '@/components/ContentAnswer.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    ContentAnswer
  }
}
</script>
