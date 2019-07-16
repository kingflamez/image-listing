<template>
  <div class="modal">
    <div class="close" @click="$emit('close')">
      <close />
    </div>
    <div class="modal__body">
      <img :src="photo.urls.regular" :alt="photo.description" />
      <div class="footer">
        <h3 class="name">
          {{ photo.user.first_name }} {{ photo.user.last_name }}
        </h3>
        <p class="location">{{ photo.user.location }}</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba($color: #000000, $alpha: 0.6);
  z-index: 99;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 50px;
  @include respond-phone {
    padding: 0;
  }
  .close {
    position: absolute;
    top: 20px;
    padding: 20px;
    cursor: pointer;
    right: 40px;
    @include respond-phone {
      top: 5px;
      right: 5px;
      padding: 10px;
      background-color: rgba($color: #000000, $alpha: 0.8);
      height: 40px;
      width: 40px;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 20px;
    }
    svg {
      height: 25px;
      @include respond-phone {
        height: 15px;
      }
    }
    transition: all 500ms;
    &:hover {
      transform: scale(0.8);
    }
  }
  &__body {
    max-width: 900px;
    background: white;
    width: 100%;
    height: 100%;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    @include respond-phone {
      border-radius: 0;
    }
    overflow: hidden;
    img {
      object-fit: cover;
      height: 83%;
      width: 100%;
      @include respond-phone {
        object-fit: contain;
      }
    }
    .footer {
      display: flex;
      padding: 20px;
      flex: 1;
      justify-content: center;
      flex-direction: column;
      .name {
        color: #2a3d5b;
        font-size: 1.5rem;
        margin-bottom: 10px;
        font-weight: 600;
      }
      .location {
        color: #7d889c;
        font-size: 14px;
        font-weight: 600;
      }
    }
  }
}
</style>

<script>
import Close from '~/components/svg/close'

export default {
  components: {
    Close
  },
  props: {
    photo: {
      default: () => {},
      type: Object
    }
  }
}
</script>
