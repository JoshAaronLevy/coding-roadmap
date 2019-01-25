<template>
  <div id="blog-home" class="section">
    <div class="container">
      <h2 class="is-size-1">Articles</h2>
      <div class="columns is-multiline">
        <div class="column is-one-third" v-for="(post,index) in posts" :key="post.slug + '_' + index">
          <div class="box">
            <article class="media">
              <div class="media-left">
                <router-link :to="'/' + post.slug">
                  <figure class="image is-64x64">
                    <img class="thumb" v-if="post.featured_image" :src="post.featured_image" alt="">
                    <img class="thumb" v-else src="http://via.placeholder.com/250x250" alt="">
                  </figure>
                </router-link>
              </div>
              <div class="media-content">
                <div class="content">
                  <router-link :to="'/' + post.slug">
                    <h2 class="title is-5">{{ post.title }}</h2>
                  </router-link>
                  <p class="post-summary">{{ post.summary }}</p>
                </div>
              </div>
            </article>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
  
<script>
  import { butter } from '@/buttercms'
  export default {
    name: 'blog-home',
    data() {
      return {
        page_title: 'Blog',
        posts: [],
        categories: []
      }
    },
    methods: {
      getPosts() {
        butter.post.list({
          page: 1,
          page_size: 10
        }).then((res) => {
          this.posts = res.data.data
        })
      },
      getCategories() {
        butter.category.list()
          .then((res) => {
            console.log('List of Categories:')
            console.log(res.data.data)
          })
      },
      getPostsByCategory() {
        butter.category.retrieve('example-category', {
            include: 'recent_posts'
          })
          .then((res) => {
            console.log('Posts with specific category:')
            console.log(res)
          })
      }
    },
    created() {
      this.getPosts()
      this.getCategories()
      this.getPostsByCategory()
    }
  }
</script>

<style>
.md-toolbar.md-theme-default.md-primary {
  background-color: #368cbf !important;
}
.md-theme-default a {
  color: #368cbf !important;
}

.md-theme-default a:hover {
  text-decoration: none !important;
  color: #33363b !important;
}

.md-title {
  font-size: 22px !important;
}

.md-title a {
  color: #FFFFFF !important;
}

.md-title a:hover {
  color: #FFFFFF !important;
}

.md-theme-default :not(input):not(textarea)::selection {
  background-color: #368cbf !important;
  color: #FFFFFF !important;
}

.media-left img:not(.md-image) {
  max-width: 250px;
}
.media-left img.thumb {
  max-width: 250px !important;
}
.media {
  display: flex;
  padding-bottom: 40px;
  padding-top: 40px;
  border-top: 1px solid;
}
body {
  line-height: 26px !important;
  --md-theme-default-accent: #368cbf !important;
}
p {
  font-size: 16px !important;
  margin-top: 30px !important;
  margin-bottom: 30px !important;
}
p.post-summary {
  padding-right: 80px;
}

</style>