<script setup lang="ts">
import {
  SbButton,
  SbCard,
  SbCardContent,
  SbCardHeader,
  SbFormItem,
  SbGroupButton,
  SbIconButton,
  SbSelect,
  SbTextField,
} from '@storyblok/design-system'
import { ref, watch } from 'vue'

const themes = ['default', 'dark', 'light-high-contrast', 'dark-high-contrast']
const selectedTheme = ref('default')

const clicks = ref(0)
const email = ref('')
watch(
  selectedTheme,
  (newTheme) => {
    document.documentElement.setAttribute('theme', newTheme ?? 'default')
  },
  { immediate: true },
)

const handleSubmit = () => {
  if (email.value === '') {
    alert('Please enter an email address')
    return
  }

  alert('Form submitted with email: ' + email.value)
}
</script>

<template>
  <div class="container">
    <h1 class="text-heading-3xl">Design System Playground</h1>

    <SbFormItem class="sb-mt-4" label="Select a theme">
      <SbSelect v-model="selectedTheme" :options="themes" />
    </SbFormItem>

    <SbCard class="sb-mb-4">
      <SbCardHeader title="How many times did you click?" />
      <SbCardContent>
        <p class="text-body-xl-regular">You clicked {{ clicks }} times</p>

        <SbGroupButton appearance="filled" variant="primary">
          <SbButton label="Click me" @click="clicks++" />
          <SbIconButton label="Reset" icon="refresh-ccw" @click="clicks = 0" />
        </SbGroupButton>
      </SbCardContent>
    </SbCard>

    <SbCard>
      <SbCardContent>
        <h3 class="text-heading-md">Sign up for our newsletter</h3>
        <form @submit.prevent="handleSubmit">
          <SbFormItem>
            <SbTextField v-model="email" label="Email" type="email" />
          </SbFormItem>

          <SbButton label="Sign up" variant="primary" />
        </form>
      </SbCardContent>
    </SbCard>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: var(--sb-size-spacing-xl);
  background-color: var(--sb-color-background-primary);
}
</style>
