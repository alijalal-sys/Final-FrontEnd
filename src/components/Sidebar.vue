<template lang="html">
  <div id="parentx">
    <vs-sidebar
      v-model="active"
      hidden-background="true"
      static-position="fixed"
      :reduce="reduce"
      :reduce-not-hover-expand="notExpand"
      parent="body"
      default-index="1"
      color="success"
      class="sidebarx"
      spacer
    >
      <div
        slot="header"
        class="header-sidebar"
      >
        <vs-avatar
          size="70px"
          src="https://randomuser.me/api/portraits/men/85.jpg"
        />
      </div>
      <vs-sidebar-group
        open
        title="Application"
      >
        <vs-sidebar-item
          index="1"
          icon="menu"
          @click="reduce=!reduce"
        >
          Toggle Sidebar
        </vs-sidebar-item>
        <vs-sidebar-item
          index="5"
          icon="verified_user"
        >
          Configurations
        </vs-sidebar-item>
        <vs-sidebar-group title="Store">
          <vs-sidebar-item
            index="2.1"
            icon="store"
          >
            Store
          </vs-sidebar-item>
          <vs-sidebar-item
            index="2.2"
            icon="nature_people"
          >
            Nature
          </vs-sidebar-item>
          <vs-sidebar-item
            index="2.3"
            icon="style"
          >
            Style
          </vs-sidebar-item>
        </vs-sidebar-group>
        <vs-sidebar-item
          index="2"
          icon="gavel"
        >
          History
        </vs-sidebar-item>
        <vs-sidebar-item
          index="3"
          icon="https"
        >
          Security
        </vs-sidebar-item>
        <vs-sidebar-item
          index="4"
          icon="help"
        >
          Help
        </vs-sidebar-item>
      </vs-sidebar-group>


      <vs-divider
        icon="person"
        position="left"
      >
        User
      </vs-divider>


      <vs-sidebar-item
        index="6"
        icon="account_box"
      >
        Profile
      </vs-sidebar-item>

      <div
        slot="footer"
        class="footer-sidebar"
      >
        <vs-button
          icon="settings"
          color="primary"
          type="border"
        />
      </div>
    </vs-sidebar>
  </div>
</template>

<script>
export default {
  name: 'Sidebar',
  data:()=>({
    active:false,
    notExpand: false,
    reduce: true
  })
}
</script>

<style lang="stylus">
.header-sidebar
  display flex
  align-items center
  justify-content center
  flex-direction column
  width 100%
  h4
    display flex
    align-items center
    justify-content center
    width 100%
    > button
      margin-left 10px
.footer-sidebar
  display flex
  align-items center
  justify-content space-between
  width 100%
  > button
      border 0px solid rgba(0,0,0,0) !important
      border-left 1px solid rgba(0,0,0,.07) !important
      border-radius 0px !important
</style>