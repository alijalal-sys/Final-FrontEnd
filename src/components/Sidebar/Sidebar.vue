<template>
  <nav
    :class="{sidebar: true, sidebarStatic, sidebarOpened}"
    @mouseenter="sidebarMouseEnter"
    @mouseleave="sidebarMouseLeave"
  >
    <header class="logo">
      <router-link to="/app">
        <span class="text-warning">Motus</span> App
      </router-link>
    </header>
    <ul class="nav">
      <NavLink
        header="Home"
        link="/app/dashboard"
        icon-name="flaticon-home"
        index="dashboard"
        is-header
      />
      <NavLink
        header="Charts"
        link="/app/charts"
        icon-name="flaticon-list"
        index="charts"
        is-header
      />
      <NavLink
        header="Probabilities"
        link="/app/probabilities"
        icon-name="flaticon-file-2"
        index="probabilities"
        is-header
      />
      <NavLink
        header="Add New User"
        link="/app/adduser"
        icon-name="flaticon-add-1"
        index="adduser"
        is-header
      />
      <NavLink
        header="Download All Data"
        link="/app/alldata"
        icon-name="flaticon-download"
        index="alldata"
        is-header
      />
      <!-- <NavLink
        :active-item="activeItem"
        header="Components"
        link="/app/components"
        icon-name="flaticon-network"
        index="components"
        :children-links="[
          { header: 'Icons', link: '/app/components/icons' },
        ]"
      /> -->
    </ul>
  </nav>
</template>

<script>
import { mapState, mapActions } from 'vuex';
import isScreen from '../../core/screenHelper.js';
import NavLink from './NavLink/NavLink';

export default {
  name: 'Sidebar',
  components: { NavLink },
  data() {
    return {
      alerts: [
        {
          id: 0,
          title: 'Sales Report',
          value: 15,
          footer: 'Calculating x-axis bias... 65%',
          color: 'info',
        },
        {
          id: 1,
          title: 'Personal Responsibility',
          value: 20,
          footer: 'Provide required notes',
          color: 'danger',
        },
      ],
    };
  },
  methods: {
    ...mapActions('layout', ['changeSidebarActive', 'switchSidebar']),
    setActiveByRoute() {
      const paths = this.$route.fullPath.split('/');
      paths.pop();
      this.changeSidebarActive(paths.join('/'));
    },
    sidebarMouseEnter() {
      if (!this.sidebarStatic && (isScreen('lg') || isScreen('xl'))) {
        this.switchSidebar(false);
        this.setActiveByRoute();
      }
    },
    sidebarMouseLeave() {
      if (!this.sidebarStatic && (isScreen('lg') || isScreen('xl'))) {
        this.switchSidebar(true);
        this.changeSidebarActive(null);
      }
    },
  },
  created() {
    this.setActiveByRoute();
  },
  computed: {
    ...mapState('layout', {
      sidebarStatic: state => state.sidebarStatic,
      sidebarOpened: state => !state.sidebarClose,
      activeItem: state => state.sidebarActiveElement,
    }),
  },
};
</script>

<!-- Sidebar styles should be scoped -->
<style src="./Sidebar.scss" lang="scss" scoped/>
