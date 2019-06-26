<template>
  <v-footer
    id="core-footer"
    absolute
    height="82"
  >
    <div class="footer-items">
      <span
        v-for="link in links"
        :key="link.name"
      >
        <a
          :href="link.Link"
          class="tertiary--text footer-links">{{ link.name }}</a>
      </span>
    </div>
    <v-spacer/>
    <span class="font-weight-light copyright">
      &copy;
      {{ (new Date()).getFullYear() }}
      <a
        href="https://www.facebook.com/esaksham"
        target="_blank">Saksham Gupta</a>, made with
      <v-icon
        color="tertiary"
        size="17">mdi-heart</v-icon>
      for ZoloStays
    </span>
  </v-footer>
</template>

<script>
export default {
  data: () => ({
    links: [
      { name: 'Home', Link: '/dashboard' },
      { name: 'Saksham Gupta', Link: 'https://www.github.com/saksham2410' },
      { name: 'About Zolo', Link: 'https://github.com/saksham2410' },
      { name: 'Meow', Link: 'https://github.com' }
    ]
  })
}
</script>

<style>
#core-footer {
  z-index: 0;
}
</style>
