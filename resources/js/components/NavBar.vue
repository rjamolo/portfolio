<template>
  <nav v-show="isNavBarVisible" id="navbar-main" class="navbar is-fixed-top">
    <div class="navbar-brand">
      <a class="navbar-item is-hidden-tablet-only is-hidden-mobile" @click.prevent="menuToggleDesktop">
        <b-icon :icon="menuToggleDesktopIcon"/>
      </a>
    </div>
    <div class="navbar-brand is-right">
      <a class="navbar-item navbar-item-menu-toggle is-hidden-desktop" @click.prevent="menuNavBarToggle">
        <b-icon :icon="menuNavBarToggleIcon" custom-size="default"/>
      </a>
    </div>
    <div class="navbar-menu fadeIn animated faster" :class="{'is-active':isMenuNavBarActive}">
      <div class="navbar-end">
        <nav-bar-menu class="has-divider has-user-avatar">
          <user-avatar/>
          <div class="is-user-name">
            <span>{{ userName }}</span>
          </div>

          <div slot="dropdown" class="navbar-dropdown">
            <router-link
              to="/profile"
              class="navbar-item"
              exact-active-class="is-active"
            >
              <b-icon icon="account" custom-size="default" />
              <span>My Profile</span>
            </router-link>
            <a class="navbar-item">
              <b-icon icon="settings" custom-size="default"></b-icon>
              <span>Settings</span>
            </a>
            <a class="navbar-item">
              <b-icon icon="email" custom-size="default"></b-icon>
              <span>Messages</span>
            </a>
            <hr class="navbar-divider" />
            <a class="navbar-item" @click="logout">
              <b-icon icon="logout" custom-size="default"></b-icon>
              <span>Logout</span>
            </a>
          </div>
        </nav-bar-menu>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapState } from 'vuex'
import NavBarMenu from '@/components/NavBarMenu'
import UserAvatar from '@/components/UserAvatar'

export default {
  name: 'NavBar',
  components: {
    UserAvatar,
    NavBarMenu
  },
  data () {
    return {
      isMenuNavBarActive: false,
    }
  },
  computed: {
    menuNavBarToggleIcon () {
      return this.isMenuNavBarActive ? 'close' : 'dots-vertical'
    },
    menuToggleMobileIcon () {
      return this.isAsideMobileExpanded ? 'backburger' : 'forwardburger'
    },
    menuToggleDesktopIcon () {
      return this.isAsideDesktopExpanded ? 'backburger' : 'forwardburger'
    },
    ...mapState(['isNavBarVisible', 'isAsideMobileExpanded', 'isAsideDesktopExpanded', 'userName'])
  },
  methods: {
    menuToggleMobile () {
      this.$store.commit('asideMobileStateToggle')
    },
    menuToggleDesktop () {
      this.$store.commit('asideDesktopStateToggle')
    },
    menuNavBarToggle () {
      this.isMenuNavBarActive = !this.isMenuNavBarActive
    },
    logout () {
      document.getElementById('logout-form').submit()
    }
  }
}
</script>
