<template>
  <v-fade-transition mode="out-in">
    <router-view v-if="languageIsValid" />
    <not-found-page v-else to="/en/" />
  </v-fade-transition>
</template>

<script>
  import languages from '@/data/i18n/languages.json'
  import NotFoundPage from '@/pages/general/404Page.vue'

  const fallbackLocale = languages.find(lang => lang.fallback === true).locale

  export default {
    components: {
      NotFoundPage
    },

    props: {
      lang: {
        type: String,
        default: fallbackLocale
      }
    },

    data: () => ({
      availableLocales: languages.map(lang => lang.locale),
      languages
    }),

    computed: {
      languageIsValid () {
        return this.availableLocales.includes(this.lang)
      }
    }
  }
</script>
