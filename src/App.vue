<template>
  <div id="restaurant-forum">
    <!-- Navbar -->
    <Navbar />

    <main role="main" class="mt-5 bg-white">
      <router-view />
    </main>

    <!-- Footer -->
    <Footer />

  </div>
</template>

<script>
import Navbar from './components/Navbar'
import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    Navbar,
    Footer
  }
}
</script>
