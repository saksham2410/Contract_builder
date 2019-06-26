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
        href="https://www.creative-tim.com/"
        target="_blank">Saksham Gupta</a>, made for
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
      { name: 'Saksham Gupta', Link: 'https://www.creative-tim.com' },
      { name: 'About Zolo', Link: 'https://creative-tim.com/presentation' },
      { name: 'Meow', Link: 'https://blog.creative-tim.com' }
    ]
  })
}
</script>

<style>
#core-footer {
  z-index: 0;
}
</style>
