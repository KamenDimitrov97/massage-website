<template>
  <section
    id="calendar"
    v-if="selectedService"
    class="p-8 bg-gray-50 opacity-0 transition-opacity duration-1000"
    :class="{ 'opacity-100': inView }"
    ref="section"
  >
    <h2 class="text-center text-3xl font-semibold mb-8">Contact Us</h2>
    <form class="max-w-xl mx-auto bg-white p-6 rounded-lg shadow-lg">
      <div class="mb-4">
        <label class="block text-gray-600 mb-2">Name</label>
        <input type="text" class="w-full border rounded-lg p-2" />
      </div>
      <div class="mb-4">
        <label class="block text-gray-600 mb-2">Email</label>
        <input type="email" class="w-full border rounded-lg p-2" />
      </div>
      <div class="mb-4">
        <label class="block text-gray-600 mb-2">Preferred Date</label>
        <input type="date" class="w-full border rounded-lg p-2" />
      </div>
      <button
        type="submit"
        class="bg-green-500 text-white px-6 py-2 rounded-full"
      >
        Book Appointment
      </button>
    </form>
  </section>
</template>

<script>
import { useIntersectionObserver } from '@vueuse/core';

export default {
  props: ['selectedService'],
  data() {
    return {
      inView: false,
    };
  },
  mounted() {
    const { stop } = useIntersectionObserver(this.$refs.section, ([{ isIntersecting }]) => {
      if (isIntersecting) {
        this.inView = true;
        stop();
      }
    });
  },
};
</script>
