<template>
  <footer class="footer -mx-4 md:mx-0">
      <a href="https://github.com/Gomah/bluise">
        <img :src="rodape" alt="Logo" />
      </a>
  </footer>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import settings from '@/content/settings/general.json';
@Component
export default class Footer extends Vue {
  get pages(): Page[] {
    return this.$store.state.pages;
  }

  rodape = settings.rodape;
}
</script>

<style lang="scss">
.footer {
  background-color: $bluise;
}
</style>
