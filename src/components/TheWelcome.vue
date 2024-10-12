<script setup>
import { computed, ref, watch } from 'vue'
import WelcomeItem from './WelcomeItem.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'

const key = ref('')

const items = [
  {
    title: 'Documentation',
    body: 'Vue’s official documentation provides you with all information you need to get started.',
  },
  {
    title: 'Tooling',
    body:
      'This project is served and bundled with Vite. The recommended IDE setup is VSCode + Volar. If you need to test your components and web pages, check out Cypress and Cypress Component Testing.\n' +
      'More instructions are available in README.md.',
  },
  {
    title: 'Ecosystem',
    body: 'Get official tools and libraries for your project: Pinia, Vue Router, Vue Test Utils, and Vue Dev Tools. If you need more resources, we suggest paying Awesome Vue a visit.',
  },
  {
    title: 'Community',
    body: 'Got stuck? Ask your question on Vue Land, our official Discord server, or StackOverflow. You should also subscribe to our mailing list and follow the official @vuejs twitter account for latest news in the Vue world.',
  },
  {
    title: 'Support Vue',
    body: 'As an independent project, Vue relies on community backing for its sustainability. You can help us by becoming a sponsor.',
  },
]

const highlightText = str => {
  if (key.value === '') return str
  return str.replaceAll(
    new RegExp(key.value, 'gi'),
    `<mark>${key.value}</mark>`,
  )
}

const filtered = computed(() =>
  items.map(item => ({
    title: highlightText(item.title),
    body: highlightText(item.body),
  })),
)
</script>

<template>
  <input v-model="key" autofocus type="text" class="" />

  <WelcomeItem v-for="(item, idx) in filtered" :key="idx">
    <template #icon>
      <DocumentationIcon />
    </template>
    <template v-slot:heading>
      <h3 v-html="item.title"></h3>
    </template>
    <div v-html="item.body"></div>
  </WelcomeItem>
</template>

<style>
input {
  background-color: #2c3e50;
  border: 1px solid #999;
  border-radius: 4px;
  color: #999999;
  height: 36px;
  padding: 0 16px;
  font-size: larger;
  width: 100%;
}
</style>
