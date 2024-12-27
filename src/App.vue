<template>
  <div>
    <HeroSection />
    <AboutSection />
    <ServicesSection
      @service-selected="onServiceSelected"
      :selectedService="selectedService"
    />
    <CalendarSection
      v-if="selectedService"
      :selectedService="selectedService"
    />
  </div>
</template>

<script>
import HeroSection from './components/HeroSection.vue';
import AboutSection from './components/AboutSection.vue';
import ServicesSection from './components/ServicesSection.vue';
import CalendarSection from './components/CalendarSection.vue';

export default {
  components: {
    HeroSection,
    AboutSection,
    ServicesSection,
    CalendarSection,
  },
  data() {
    return {
      selectedService: null,
    };
  },
  methods: {
    onServiceSelected(service) {
      this.selectedService = service; // Update selected service

      // Wait until the next DOM update, then scroll to the calendar section
      this.$nextTick(() => {
        const calendarElement = document.getElementById('calendar');
        if (calendarElement) {
          calendarElement.scrollIntoView({ behavior: 'smooth' });
        }
      });
    },
  },
};
</script>
