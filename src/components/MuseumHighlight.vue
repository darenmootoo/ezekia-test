<template>
  <div
    class="museum-highlight"
    :class="{ 'museum-highlight__partner': details.origin === 'spacePartner' }"
  >
    <!-- Display the available information for the highlight -->
    <div class="museum-highlight__content">
      <font-awesome-icon
        v-if="cornerImage"
        :icon="cornerImage"
        class="museum-highlight__corner-image"
        size="2x"
      />
      <img
        class="museum-highlight__image"
        :src="details.image || 'https://via.placeholder.com/300'"
        :alt="details.name"
      />
      <h2>{{ details.name }}</h2>
      <div class="museum-highlight__card-content">
        <p>{{ details.description }}</p>
        <h3 v-if="details?.news">News</h3>
        <p v-if="details?.news?.date">Date: {{ details.news.date }}</p>
        <p v-if="details?.news?.title">{{ details.news.title }}</p>
        <div v-if="details?.quiz">
          <span>Quiz: </span><a :href="details.quiz">{{ details.quiz }}</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MuseumHighlight",
  components: {},
  mixins: [],
  props: {
    details: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {};
  },
  computed: {
    newsDate() {
      // Highlight's news item date
      if (!this.details?.news?.date) return null;
      return new Date(this.details.news.date);
    },
    cornerImage() {
      if (this.details.page === "space") return "fa-solid fa-star";
      return null;
    },
  },
  methods: {},
  created() {},
};
</script>

<style lang="scss" scoped>
.museum-highlight {
  width: 400px;
  height: 300px;
  overflow: hidden;
  margin: 10px 20px;

  p,
  h2,
  h3 {
    margin-bottom: 5px;
  }

  h2 {
    margin-top: 5px;
  }

  h3 {
    text-decoration: underline;
  }

  &__card-content {
    height: 74px;
  }

  &__content {
    display: flex;
    flex-direction: column;
    padding: 10px;
    overflow: auto;
    height: 100%;
    width: 100%;
  }

  &__partner {
    border: 2px dotted var(--star);
  }

  &__corner-image {
    position: absolute;
    top: 0;
    right: 0;
    color: var(--star);
    z-index: 1;
  }

  &__image {
    width: 350px;
    height: 200px;
    object-fit: cover;
    margin: 0 auto;
  }
}
</style>
