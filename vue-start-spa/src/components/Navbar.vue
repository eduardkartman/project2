<template>
  <nav :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']">
  <div class="container-fluid">
    <a class="navbar-brand" href="#"> My Vue</a>
    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
      <li
        v-for="(page,index) in publishedPages"
        class="nav-item"
        :key="index">
        <navbar-link
          :page="page"
          :isActive="activePage === index"
          @click.prevent="navLinkClick(index)">
        </navbar-link>
      </li>
    </ul>
    <form class="d-flex">
      <button class="btn btn-dark" @click.prevent="changeTheme()">Toggle</button>
    </form>
  </div>
</nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue'

export default {
  props: ['pages', 'activePage', 'navLinkClick'],
  components: {
    NavbarLink
  },
  computed: {
    publishedPages () {
      return this.pages.filter(p => p.published)
    }
  },
  data () {
    return {
      theme: 'light'
    }
  },
  created () {
    this.getThemeSetting()
  },
  methods: {
    changeTheme () {
      let theme = 'light'

      if (this.theme === 'light') {
        theme = 'dark'
      }
      this.theme = theme
      this.storeThemeSetting()
    },
    storeThemeSetting () {
      localStorage.setItem('theme', this.theme)
    },
    getThemeSetting () {
      const theme = localStorage.getItem('theme', this.theme)
      if (theme) {
        this.theme = theme
      }
    }
  }
}
</script>

<style scoped>
.emphasize {
  text-decoration: underline !important;
}
</style>
