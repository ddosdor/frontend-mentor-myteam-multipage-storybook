<template>
  <div class="flex flex-col flex-grow justify-end">
    <SectionsHeroSection v-once />
    <SectionsBenefitsSection v-once />
    <SectionsSuccessStoriesSection v-once />
    <SectionsCtaSection />
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api';

export default defineComponent({
  name: 'HomePage',
});
</script>
