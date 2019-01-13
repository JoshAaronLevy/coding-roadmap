<template>
  <div class="page-container">
    <md-app md-waterfall md-mode="overlap">
      <md-app-toolbar class="md-primary md-large">
        <div class="md-toolbar-row">
          <md-button class="md-icon-button" @click="menuVisible = !menuVisible">
            <md-icon>menu</md-icon>
          </md-button>
          <span class="md-title"><router-link to="/">Coding Roadmap</router-link></span>
          <!-- <md-button class="md-primary">Login</md-button> -->
        </div>
      </md-app-toolbar>
      <md-app-drawer :md-active.sync="menuVisible">
        <md-toolbar class="md-transparent" md-elevation="0">
          Navigation
        </md-toolbar>
        <md-list>
          <md-list-item>
            <md-icon>list</md-icon>
            <span class="md-list-item-text">Articles</span>
          </md-list-item>
          <md-list-item>
            <md-icon>view_module</md-icon>
            <span class="md-list-item-text">Categories</span>
          </md-list-item>
          <md-list-item>
            <md-icon>label</md-icon>
            <span class="md-list-item-text">Tags</span>
          </md-list-item>
        </md-list>
      </md-app-drawer>
      <md-app-content>
        <router-view/>
      </md-app-content>
    </md-app>
    <md-toolbar class="md-dense">
      <h4 class="copy">Copyright 2019 - Josh Levy</h4>
      <h4 class="copy">Content Managed With <a href="https://buttercms.com/" target="_blank">ButterCMS</a></h4>
    </md-toolbar>
  </div>
</template>

<style lang="scss" scoped>
  .md-app {
    min-height: 100vh;
    border: 1px solid rgba(#000, .12);
  }

  body {
    line-height: 26px !important;
  }

  p {
    font-size: 16px !important;
  }

  .md-toolbar.md-theme-default.md-primary {
    height: 120px;
  }

  .md-title a {
    color: #fff !important;
  }

  .md-theme-default a {
    color: #fff;
  }

  .md-theme-default a:hover {
    text-decoration: none;
    color: #fff;
  }

  .md-app.md-overlap .md-app-content {
    margin: -50px 24px 24px !important;
  }

  // Demo purposes only
  .md-drawer {
    width: 230px;
    max-width: calc(100vw - 125px);
  }

  .copy {
    margin: 0px;
  }

  .md-dense {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .md-dense a {
    color: #333;
  }
</style>

<script>
export default {
  name: 'Overlap',
  data: () => ({
    menuVisible: false
  })
}
</script>
