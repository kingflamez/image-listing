<template>
  <div class="body">
    <section class="header">
      <div class="container">
        <div class="header__searchBox">
          <div class="header__searchBox__icon">
            <search />
          </div>
          <input
            v-model="search"
            placeholder="Search for photo"
            @keyup.enter="searchPhoto()"
          />
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
import Search from '~/components/svg/search'
import Modal from '~/components/modal'

export default {
  components: {
    Search,
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
    const photos = await this.$axios.$get(`search/photos?query=African`, {
      headers: {
        Authorization: `Client-ID ${process.env.UNSPLASH_ACCESS_KEY}`
      }
    })
    photos.results.map(p => {
      p.spanLength = this.generateSpan()
    })
    this.photos = photos.results
    this.loading = false
  },
  methods: {
    closeModal() {
      this.showModal = false
      this.selectedPhoto = {}
    },
    generateSpan() {
      let gen = Math.floor(Math.random() * 8)
      do {
        gen = Math.floor(Math.random() * 8)
      } while (gen < 4)
      return gen
    },
    searchPhoto() {
      if (this.search.length > 0) {
        this.$router.push(`/search?query=${this.search}`)
      }
    },
    openPhoto(photo) {
      this.selectedPhoto = photo
      this.showModal = true
    }
  }
}
</script>
