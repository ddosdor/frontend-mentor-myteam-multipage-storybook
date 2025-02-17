<template>
  <component :is="asNuxtLink ? 'nuxt-link' : 'button'"
             class="UiButton"
             :class="{
               'UiButton--primary': buttonType === 'primary',
               'UiButton--primaryDark': buttonType === 'primaryDark',
               'UiButton--secondary': buttonType === 'secondary',
               'UiButton--as-link': asNuxtLink,
             }"
             :disabled="disabled"
             :to="to"
             @click="$emit('click')"
  >
    <slot />
  </component>
</template>

<script lang="ts">
import { defineComponent, ref } from '@nuxtjs/composition-api';

export default defineComponent({
  name: 'UiButton',
  props: {
    /**
     * Set button as primary type
     */
    primary: Boolean,
    /**
     * Set button as primary-dark type
     */
    primaryDark: Boolean,
    /**
     * Set button as secondary
     */
    secondary: Boolean,
    /**
     * Set button as link (NuxtLink)
     */
    asNuxtLink: Boolean,
    /**
     * Page url if button is used as a nuxt-link
     */
    to: {
      type: String,
      default: null,
    },
    /**
     * Set button as disabled
     */
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['click'],
  setup(props) {
    const buttonType = ref<String>('primary');
    switch (true) {
      case props.primary: buttonType.value = 'primary'; break;
      case props.primaryDark: buttonType.value = 'primaryDark'; break;
      case props.secondary: buttonType.value = 'secondary'; break;
      default: buttonType.value = 'primary';
    }

    return { buttonType };
  },
});
</script>

<style lang="sass" scoped>
.UiButton
  @apply border-2 px-8 rounded-3xl h-12 transition-colors duration-150 block
  @apply disabled:cursor-not-allowed disabled:opacity-20

  &--as-link
    @apply leading-[43px]

  &--primary
    @apply border-primary-white text-primary-white
    @apply hover:bg-primary-white hover:text-primary-midnightGreen
    @apply disabled:bg-transparent disabled:text-primary-white

  &--primaryDark
    @apply border-secondary-sacramentoStateGreen bg-transparent text-secondary-sacramentoStateGreen
    @apply hover:bg-secondary-sacramentoStateGreen hover:border-secondary-sacramentoStateGreen hover:text-primary-white
    @apply disabled:border-secondary-sacramentoStateGreen disabled:bg-transparent disabled:text-secondary-sacramentoStateGreen

  &--secondary
    @apply border-primary-white bg-primary-white text-primary-midnightGreen
    @apply hover:border-secondary-raptureBlue hover:bg-secondary-raptureBlue
    @apply disabled:border-primary-white disabled:bg-primary-white disabled:text-primary-midnightGreen
</style>
