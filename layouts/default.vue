<template>
  <div>
    <nuxt />
  </div>
</template>

<style lang="scss">
$container-horizontal: 20px;
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding-left: $container-horizontal;
  padding-right: $container-horizontal;
}

$vertical-padding: 200px;
$mvertical-padding: 140px;
.images__item:hover {
  transform: scale(1.1);
}
.body {
  padding-bottom: 100px;
}
.header {
  background-color: #dde2e9;
  padding-top: $vertical-padding;
  padding-bottom: $vertical-padding;
  @include respond-phone {
    padding-top: $mvertical-padding;
    padding-bottom: $mvertical-padding;
  }
  &__title {
    color: #263958;
    font-weight: bold;
    font-size: 2.2rem;
    &__search {
      color: #6c7a91;
    }
  }
  &__searchBox {
    position: relative;
    &__icon {
      position: absolute;
      left: 0;
      height: 100%;
      width: 60px;
      padding: 19px;
      display: flex;
      align-items: center;
      justify-content: center;
      svg {
        height: 100%;
        width: auto;
      }
    }
    input {
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      border-radius: 5px;
      background-color: #fff;
      box-shadow: 0 0 15px 10px rgba(0, 0, 0, 0.05);
      border: 0;
      width: 100%;
      font-size: 16px;
      padding: 20px;
      padding-left: 60px;
      outline: 0;
    }
  }
}

.images {
  max-width: 980px;
  margin: 0 auto;
  display: grid;
  margin-top: -130px;
  @include respond-phone {
    margin-top: -90px;
  }
  grid-row-gap: 30px;
  column-gap: 40px;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-auto-rows: 40px;
  @include respond-phone {
    grid-template-columns: 1fr;
  }

  &__loader {
    height: 100%;
    width: 100%;
    background-size: cover;
    background-position: center;
    border-radius: 8px;
    position: relative;
    overflow: hidden;
    background-color: #f5f5f5;
    -webkit-animation: 1s linear infinite;
    animation: loading-glow 1s linear infinite;
    @include respond-phone {
      grid-row-end: span 5 !important;
    }
    &:nth-child(even) {
      -webkit-animation-delay: 0.6s;
      animation-delay: 0.6s;
    }
    .info {
      position: absolute;
      bottom: 20px;
      left: 20px;
      right: 20px;
      z-index: 9;
      &__name {
        width: 50%;
        height: 14px;
        background-color: #e6e6e6;
      }
      &__location {
        margin-top: 8px;
        width: 35%;
        height: 14px;
        background-color: #e6e6e6;
      }
    }
  }
  &__item {
    height: 100%;
    width: 100%;
    background-size: cover;
    background-position: center;
    border-radius: 8px;
    background-color: #f5f5f5;
    cursor: pointer;
    transition: all 500ms;
    position: relative;
    overflow: hidden;
    @include respond-phone {
      grid-row-end: span 5 !important;
    }
    img {
      object-fit: cover;
      height: 100%;
    }
    .info {
      position: absolute;
      bottom: 20px;
      left: 20px;
      right: 20px;
      z-index: 9;
      color: white;
      &__name {
        font-size: 18px;
        // font-weight: bold;
      }
      &__location {
        font-size: 13px;
        opacity: 0.7;
      }
    }
    &:hover {
      transform: scale(1.05);
    }
    .overlay {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-image: linear-gradient(
        rgba(black, 0.04),
        rgba(black, 0.2),
        rgba(black, 0.2),
        rgba(black, 0.95)
      );
    }
  }
}
@keyframes loading-glow {
  0% {
    background-color: #f5f5f5;
  }
  50% {
    background-color: #efefef;
  }
  100% {
    background-color: #f5f5f5;
  }
}
</style>
