<template>
  <div :class="['xs-text-6 md-text-5 bael-grid', {paginated: hasPagination}]">
    <div v-if="posts.length" class="r full-height browse">
      <div
        v-intersect
        v-for="(p,i) in posts"
        :key="i"
        :thumbnail="p.thumbnail"
        class="xs-border xs-border-top-none xs-border-left-none xs-p2 bcg-item"
        :style="`transition-delay:0.${i * .5}s`"
      >
        <div class="item xs-block xs-full-height xs-flex">
          <nuxt-link
            class="xs-text-center xs-flex xs-full-height xs-flex-align-center xs-flex-justify-center xs-text-center"
            :to="p.path"
          >{{p.thumbnail}}</nuxt-link>
        </div>
      </div>
        <div class="feat-wrapper" :key="`${title}-featimage`">
    <transition appear name="fade">
      <img draggable="false" class="featured-image" loading="lazy" :src="thumbnail" :alt="title" />
    </transition>
  </div>
    </div>
    <div v-else class="r full-height browse">
      <div class="xs-p2 c-100 xs-flex xs-flex-align-center xs-flex-justify-center xs-text-center">
        <div v-if="posts.length < 1 && !busy">No Results.</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
     ["title", "thumbnail"],
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
