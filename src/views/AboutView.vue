<template>
  <div class="home">
   
<h1>Welcome About Page</h1>

    <AboutMe />
  </div>
</template>

<script>
// @ is an alias to /src
import AboutMe from '@/components/AboutMe.vue'

export default {
  name: 'AboutMe',
  components: {
    AboutMe
  }
}
</script>
