<template>
  <div class="body">
    <section class="header">
      <div class="container">
        <div class="header__title">
          {{
            loading
              ? 'Searching'
              : photos.length == 0
              ? 'No result'
              : 'Search Results'
          }}
          for
          <span class="header__title__search"
            >"{{ search.charAt(0).toUpperCase() + search.slice(1) }}"</span
          >
        </div>
      </div>
    </section>
    <div class="container">
      <div v-if="!loading" class="images">
        <div
          v-for="photo in photos"
          :key="photo.id"
          :style="`grid-row-end: span ${photo.spanLength};`"
          :class="`images__item`"
          @click="openPhoto(photo)"
        >
          <img
            :src="photo.urls.small"
            style="width: 100%"
            :alt="photo.description"
          />
          <div class="overlay" />
          <div class="info">
            <div class="info__name">
              {{ photo.user.first_name }} {{ photo.user.last_name }}
            </div>
            <div class="info__location">{{ photo.user.location }}</div>
          </div>
        </div>
      </div>
      <div v-else class="images">
        <div
          v-for="x in 6"
          :key="x"
          :style="`grid-row-end: span ${generateSpan()};`"
          :class="`images__loader`"
        >
          <div class="loader" />
          <div class="info">
            <div class="info__name"></div>
            <div class="info__location"></div>
          </div>
        </div>
      </div>
    </div>
    <transition name="fade">
      <modal v-if="showModal" :photo="selectedPhoto" @close="closeModal" />
    </transition>
  </div>
</template>

<script>
import Modal from '~/components/modal'

export default {
  components: {
    Modal
  },
  data() {
    return {
      loading: true,
      photos: [],
      search: '',
      showModal: false,
      selectedPhoto: {}
    }
  },
  async created() {
    if (this.$route.query.query) {
      this.search = this.$route.query.query
    }
    const photos = await this.$axios.$get(
      `search/photos?query=${this.search}`,
      {
        headers: {
          Authorization: `Client-ID ${process.env.UNSPLASH_ACCESS_KEY}`
        }
      }
    )
    photos.results.map(p => {
      p.spanLength = this.generateSpan()
    })
    this.photos = photos.results
    this.loading = false
  },
  methods: {
    generateSpan() {
      let gen = Math.floor(Math.random() * 8)
      do {
        gen = Math.floor(Math.random() * 8)
      } while (gen < 4)
      return gen
    },
    openPhoto(photo) {
      this.selectedPhoto = photo
      this.showModal = true
    },
    closeModal() {
      this.showModal = false
      this.selectedPhoto = {}
    }
  }
}
</script>
