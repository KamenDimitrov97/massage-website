<template>
  <section
    ref="section"
    class="h-screen bg-cover bg-center flex flex-col justify-center items-center text-white opacity-0 transition-opacity duration-1000"
    :class="{ 'opacity-100': inView }"
    :style="{ backgroundImage: `url(${heroImage})` }"
  >
    <h1 class="text-4xl md:text-6xl font-bold mb-4">Relax and Rejuvenate</h1>
    <button
      class="bg-green-500 hover:bg-green-600 text-white px-6 py-2 rounded-full text-lg"
      @click="scrollToSection('services')"
    >
      Book Now
    </button>
  </section>
</template>

<script>
import { useIntersectionObserver } from '@vueuse/core';

export default {
  data() {
    return {
      heroImage: require('../assets/relax.jpg'),
      inView: false,
    };
  },
  methods: {
    scrollToSection(id) {
      const element = document.getElementById(id);
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
      }
    },
  },
  mounted() {
    const { stop } = useIntersectionObserver(this.$refs.section, ([{ isIntersecting }]) => {
      if (isIntersecting) {
        this.inView = true;
        stop(); // Stop observing once visible
      }
    });
  },
};
</script>
