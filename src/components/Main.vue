<template>
  <main>
    <Elements
      @genreFilter="addGenreValue"
    />

    <div class="container">
      <div class="row justify-content-center py-5" v-if="this.loading == true">
        <div class="col col-2"
          v-for="music in filteredArrayMusics"
          :key="music.ident">
          <div class="card p-3">
            <div class="image">
              <img class="img-fluid" :src="music.poster" alt="Poster" />
            </div>
            <div class="title">
              <h4 class="text-center text-white text-uppercase fs-5">
                {{ music.title }}
              </h4>
            </div>
            <div class="author">
              <span> {{ music.author }} </span>
            </div>
            <div class="year">
              <span> {{ music.year }} </span>
            </div>
          </div>
        </div>
      </div>
      <div class="loading" v-else>
        <h1 class="text-light text-center">LOADING...</h1>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import Elements from "./Elements.vue";

export default {
  components: {
    Elements,
  },

  data() {
    return {
      musics: [],
      loading: false,
      valueSelected: "",
    };
  },

  mounted() {
    setTimeout(this.callMusicApi, 3000);
  },

  methods: {
    callMusicApi() {
      axios
        .get("https://flynn.boolean.careers/exercises/api/array/music")

        .then((r) => {
          this.musics = r.data.response;
          this.loading = true;
        })

        .catch((e) => {
          console.log(e, "Non funge");
        });
    },
    addGenreValue(genreValue) {
      
      this.valueSelected = genreValue;
    },
  },

  computed: {
    filteredArrayMusics() {
      if (this.valueSelected == "") {
        return this.musics;
      }

      const arrayMusicFiltered = this.musics.filter((music) => {
        return music.genre.includes(this.valueSelected);
      });

      return arrayMusicFiltered;
    },
  },
};
</script>

<style scoped lang="scss">
main {
  background-color: #1e2d3b;
  min-height: calc(100vh - 80px);

  .row {
    .col {
      .card {
        margin-top: 16px;
        height: 320px;
        width: 180px;
        background: rgba(255, 255, 255, 0.088);
        text-align: center;

        .image {
          margin-bottom: 16px;
        }

        .title {
          color: white;
        }

        .author,
        .year {
          color: gray;
        }

      }
    }
  }
}
</style>
