<template>
  <transition name="fade">
    <div :class="{'loading': loading, 'apod-image': true}" v-if="!loading && imageData.url">
      <h3>{{ imageData.title }}</h3>
      <div class="image-wrapper">
        <div class="image">
          <img
            v-if="!imageData.isVideo"
            :src="imageData.url"
            alt="Astronomy Picture of the Day from NASA"
          />
          <iframe
            v-else
            :src="imageData.url"
          />
        </div>
      </div>
      <p>
        {{ imageData.explanation }}<br>
        <br>
        hd-image:
        <a :href="imageData.hdurl || imageData.url">
          {{ imageData.hdurl || imageData.url}}
        </a>
      </p>
    </div>
  </transition>
</template>


<script>
import moment from 'moment';

export default {
  name: 'ApodImage',

  props: {
    date: {
      type: Date,
      default: () => new Date(),
      required: false,
    },
  },

  data() {
    return {
      loading: false,
      imageData: {},
    };
  },

  watch: {
    date(newDate, oldDate) {
      if (newDate !== oldDate) this.getData();
    },
  },

  computed: {
    dateString() {
      return moment(this.date).format('YYYY-MM-DD');
    },
  },

  created() {
    this.getData();
  },

  methods: {
    getData() {
      this.loading = true;
      fetch(`https://api.nasa.gov/planetary/apod?api_key=Mfp5wYtUgA1RFNAQ73bUCLYOuDssLyQH0lZ2RIac&hd=true&date=${this.dateString}`, {
        method: 'GET',
      })
        .then(response => response.json())
        .then((response) => {
          if (response.url) {
            if (response.url.slice(0, 2) === '//') response.url = `https:${response.url}`;
            const url = new URL(response.url);
            this.imageData = response;
            if (url.hostname.includes('youtube.com')) {
              this.imageData.isVideo = true;
            } else this.imageData.isVideo = false;
          }
          this.loading = false;
        })
        .catch((err) => {
          console.log(err);
          this.loading = false;
        });
    },
  },
};
</script>


<style lang="scss" scoped>
.apod-image {
  width: 100%;
  height: auto;

  .image-wrapper {
    padding: 0;
  }
    .image {
      width: 100%;
      padding-top: 65%;

      position: relative;
    }
      img,
      iframe {
        object-fit: cover;
        object-position: center;
        width: 100%;
        height: 100%;

        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
      }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
