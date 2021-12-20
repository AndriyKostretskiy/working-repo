<template>
  <div class="wrapper">
    <form class="sort">
      <input
        type="radio"
        id="image-text"
        name="sort"
        checked
        aria-checked="true"
        @change="textImage = !textImage"
      />
      <label for="image-text"
        >блоки в формате “изображения - слева, текст - справа”</label
      ><br />
      <input
        type="radio"
        id="text-image"
        name="sort"
        @change="textImage = !textImage"
      />
      <label for="text-image"
        >блоки в формате текст - слева, “изображения - справа”</label
      ><br /><br />
    </form>
    <div v-if="textImage" class="blocks">
      <div
        class="flex-container"
        v-for="itemResult in getReults()"
        :key="itemResult.original_title"
      >
        <div class="flex-item flex-item-1">
          <img :src="`${src}${itemResult.poster_path}`" alt="movie" />
        </div>
        <div class="flex-item flex-item-2">
          <p>
            <span>{{ itemResult.original_title }}</span>
          </p>
          <p>
            <span>{{ itemResult.overview }}</span>
          </p>
        </div>
      </div>
    </div>
    <div v-else class="blocks">
      <div
        class="flex-container"
        v-for="(itemResult, i) in getReults()"
        :key="itemBlock + i"
      >
        <div class="flex-item flex-item-2">
          <p>
            <span>{{ itemResult.original_title }}</span>
          </p>
          <p>
            <span>{{ itemResult.overview }}</span>
          </p>
        </div>
        <div class="flex-item flex-item-1">
          <img :src="`${src}${itemResult.poster_path}`" alt="movie" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "blocks-review",
  components: {},
  // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  data() {
    return {
      results: [],
      itemBlock: "block-",
      itemID: [],
      abc: false,
      textImage: true,
    };
  },
  props: {
    blockItems: {
      type: Number,
      default: 5,
    },
    src: {
      type: String,
      default: "https://image.tmdb.org/t/p/w185_and_h278_bestv2",
    },
  },
  mounted() {
    axios
      .get(
        "https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1"
      )
      .then((response) => (this.results = response.data.results))
      .catch((error) => console.log(error));
  },
  computed: {},
  watch: {},
  methods: {
    getReults() {
      return this.results
        .map((result) => result);
        // .sort(() => 0.5 - Math.random());
        // .sort();
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./styles/index.scss";
</style>
