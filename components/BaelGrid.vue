<template>
  <div :class="['xs-text-6 md-text-5 bael-grid', {paginated: hasPagination}]">
    <div v-if="posts.length" class="r full-height browse">
      <div
        v-intersect
        v-for="(p,i) in posts"
        :key="i"
        class="xs-border xs-border-top-none xs-border-left-none xs-p2 bcg-item"
        :style="`transition-delay:0.${i * .5}s`"
      >
        <div class="item xs-block xs-full-height xs-flex">
          <nuxt-link
            class="xs-text-center xs-flex xs-full-height xs-flex-align-center xs-flex-justify-center xs-text-center"
            :to="p.path"
          >{{p.title}}</nuxt-link>
        </div>
      </div>
    </div>
    <div v-else class="r full-height browse">
      <div class="xs-p2 c-100 xs-flex xs-flex-align-center xs-flex-justify-center xs-text-center">
        <div v-if="posts.length < 1 && !busy">No Results.</div>
      </div>
    </div>      <div class="xs-mt2 xs-p2 bcg-item">
        <div class="item xs-block xs-full-height">
          <lazy-featured-image
            v-if="post.thumbnail"
            :title="post.title"
            :thumbnail="post.thumbnail"
          />

          <h1 class="xs-py3 main-title">{{post.title}}</h1>
          <div class="xs-mt-5 bold">
            <ul class="list-unstyled xs-flex xs-flex-align-center">
              <li class="xs-inline-block xs-mr1" v-if="post.category">
                <div class="tag fill-gray-darker xs-border">
                  <nuxt-link
                    :to="`/category/${post.category.toLowerCase()}`"
                    class="tag__link text-white"
                  >{{post.category}}</nuxt-link>
                </div>
              </li>
              <li class="xs-inline-block">{{ post.date }}</li>
            </ul>
          </div>
          <div class="xs-py3 post-content text-gray-lighter">
            <nuxt-content :document="post" />
          </div>
        </div>
      </div>
  </div>
  
</template>

<script>
export default {
  props: {
    posts: {
      type: Array,
    },
    items:
    { type: Array}
  },
  data() {
    return {};
  },
  computed: {
    hasPagination() {
      return this.$store.state.pagination.active || false;
    },
  },
};
</script>

<style>
.bael-grid .bcg-item {
  opacity: 0;
  transition: 0.2s opacity ease-out;
}
.bael-grid .intersected.bcg-item {
  opacity: 1;
  transition: 0.2s opacity ease-out;
}
</style>
