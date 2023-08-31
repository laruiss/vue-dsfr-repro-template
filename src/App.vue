<script setup lang="ts">
import { ref } from 'vue'
import { useRegisterSW } from 'virtual:pwa-register/vue'

import ReloadPrompt from '@/components/ReloadPrompt.vue'

const serviceTitle = 'Service'
const serviceDescription = 'Description du service'
const logoText = ['Ministère', 'de l’intérieur']

const sourceLink = 'https://github.com/username/repo'

const quickLinks = [
  {
    label: 'Home',
    path: '/',
    icon: 'ri-home-4-line',
    iconAttrs: { color: 'var(--red-marianne-425-625)' },
  },
  {
    label: 'À propos',
    path: '/a-propos',
    class: 'fr-fi-user-line',
  },
]
const searchQuery = ref('')

const {
  offlineReady,
  needRefresh,
  updateServiceWorker,
} = useRegisterSW()

const close = () => {
  offlineReady.value = false
  needRefresh.value = false
}
</script>

<template>
  <DsfrHeader
    v-model="searchQuery"
    :service-title="serviceTitle"
    :service-description="serviceDescription"
    :logo-text="logoText"
    :quick-links="quickLinks"
    show-search
  />
  <div class="fr-container">
    <div class="flex flex-column h-full">
      <p>
        <a
          class="fr-link"
          type="button"
          icon="ri-github-fill"
          :href="sourceLink"
        >
          Aller au code source
          <VIcon name="ri-github-fill" />
        </a>
      </p>
    </div>
  </div>

  <ReloadPrompt
    :offline-ready="offlineReady"
    :need-refresh="needRefresh"
    @close="close()"
    @update-service-worker="updateServiceWorker()"
  />
</template>
