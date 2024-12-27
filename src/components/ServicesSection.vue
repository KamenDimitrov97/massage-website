<template>
  <section
    class="p-8 bg-white"
    id="services"
    ref="section"
  >
    <h2 class="text-center text-3xl font-semibold mb-8">Our Services</h2>
    <div class="grid gap-8 md:grid-cols-3">
      <div
        v-for="service in services"
        :key="service.name"
        class="bg-gray-100 p-6 rounded-lg shadow-md text-center cursor-pointer transition-transform transform hover:scale-105"
        :class="{
          'ring-4 ring-green-500': selectedService === service.name,
        }"
        @click="selectService(service.name)"
      >
        <h3 class="text-xl font-medium mb-2">{{ service.name }}</h3>
        <p class="text-gray-600 mb-4">{{ service.description }}</p>
        <p class="text-green-500 font-bold">{{ service.price }}</p>
      </div>
    </div>
  </section>
</template>

<script>
import { useIntersectionObserver } from '@vueuse/core';

export default {
  props: {
    selectedService: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      services: [
        {
          name: 'Swedish Massage',
          description: 'Relaxing full-body massage.',
          price: '$60/hr',
        },
        {
          name: 'Deep Tissue Massage',
          description: 'Targets deeper muscle layers.',
          price: '$75/hr',
        },
        {
          name: 'Hot Stone Therapy',
          description: 'Uses heated stones for therapy.',
          price: '$80/hr',
        },
      ],
      inView: false,
    };
  },
  methods: {
    selectService(serviceName) {
      this.$emit('service-selected', serviceName); // Notify parent about the selection
    },
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
