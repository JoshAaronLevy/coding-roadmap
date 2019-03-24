<template>
  <div class="page-container">
    <md-app md-waterfall md-mode="overlap">
      <md-app-toolbar class="md-primary md-large">
        <div class="md-toolbar-row">
          <!-- <md-button class="md-icon-button" @click="menuVisible = !menuVisible">
            <md-icon>menu</md-icon>
          </md-button> -->
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
            <router-link to="/">
              <md-icon>list</md-icon>
              <span class="md-list-item-text">Articles</span>
            </router-link>
          </md-list-item>
          <md-list-item>
            <router-link to="/categories">
              <md-icon>view_module</md-icon>
              <span class="md-list-item-text">Categories</span>
            </router-link>
          </md-list-item>
          <md-list-item>
            <router-link to="/tags">
              <md-icon>label</md-icon>
              <span class="md-list-item-text">Tags</span>
            </router-link>
          </md-list-item>
        </md-list>
      </md-app-drawer>
      <md-app-content>
        <router-view/>
      </md-app-content>
    </md-app>
    <md-toolbar class="md-dense">
      <h4 class="copy">Copyright 2019 - Josh Levy</h4>
      <h4 class="copy">Content Managed With <a href="https://buttercms.com/" target="_blank"><img src="https://s3-us-west-2.amazonaws.com/bad-movie-night/codingroadmap/butter-b.png" alt="ButterCMS" /></a></h4>
    </md-toolbar>
  </div>
</template>

<style lang="scss" scoped>
  .md-app {
    min-height: 100vh;
    border: 1px solid rgba(#000, .12);
  }

  .md-toolbar {
    font-size: 18px;
  }

  .md-list-item a {
    width: 100%;
    display: flex;
    align-items: center;
  }

  .md-list-item .md-icon {
    margin-right: 10px !important;
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

  .copy img {
    height: 50px;
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
