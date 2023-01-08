<template>
  <div class="space-page">
    <h1 class="space-page__title">Space</h1>
    <!-- Add the museum highlight cards based on the data provided below -->
    <div class="space-page__content">
      <MuseumHighlight
        :key="card.id"
        v-for="card in spaceHighlightsAndPartners"
        :details="card"
      />
    </div>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

import MuseumHighlight from "./MuseumHighlight.vue";

export default {
  name: "SpacePage",
  components: {
    MuseumHighlight,
  },
  mixins: [],
  props: {},
  data() {
    return {
      spaceHighlights: [
        {
          date: "2020-04-20 12:20:00",
          description:
            "Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.",
          id: 1,
          image: "",
          name: "Asteroids",
        },
        {
          date: "2020-05-20 15:50:00",
          description:
            "A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.",
          id: 9,
          image: "",
          name: "Comets",
        },
        {
          date: "2020-05-01 9:22:00",
          description:
            "The term planet is ancient, with ties to history, astrology, science, mythology, and religion.",
          id: 7,
          image: "",
          name: "Planets",
          news: {
            date: "2020-08-18 18:00:00",
            title: "Attend our talk about Jupiter with Dr. Hogarth",
          },
          quiz: "https://planetquiz.space",
        },
        {
          date: "2020-07-05 4:10:00",
          description:
            "A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.",
          id: 12,
          image: "",
          name: "Meteor showers",
          news: {
            title: "The Lyrids will peak at on April 21-22 2021, at night",
          },
        },
      ],
      spacePartners: {
        observatory: {
          createdAt: "2020-06-01 11:45:00",
          info: "The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.",
          image: "",
          name: "Mauna Kea Observatories",
        },
      },
    };
  },
  computed: {
    amendedSpacePartners() {
      // Assuming the space partner's API data comes back in the same shape

      let amendedSpacePartners = {};

      Object.keys(this.spacePartners).forEach((partner) => {
        let amendedSpacePartner = { ...this.spacePartners[partner] };
        const { createdAt, info, ...rest } = amendedSpacePartner;
        amendedSpacePartner = {
          ...rest,
          date: createdAt,
          description: info,
          id: uuidv4(),
          origin: "spacePartner",
          page: "space",
        };
        amendedSpacePartners[partner] = amendedSpacePartner;
      });
      return amendedSpacePartners;
    },
    spaceHighlightsAndPartners() {
      // Assuming there is always a date property

      const appendedHighlightWithPage = this.spaceHighlights.map(
        (highlight) => {
          return {
            ...highlight,
            page: "space",
          };
        }
      );
      const spaceHighlightsAndPartners = [
        ...appendedHighlightWithPage,
        ...Object.values(this.amendedSpacePartners),
      ];
      spaceHighlightsAndPartners.sort((a, b) => {
        return new Date(b.date) - new Date(a.date);
      });
      return spaceHighlightsAndPartners;
    },
  },
  methods: {},
  created() {},
};
</script>

<style lang="scss" scoped>
.space-page {
  padding: 20px;
  display: flex;
  flex-direction: column;

  &__title {
    margin-bottom: 20px;
    font-size: 55px;
    color: black;
  }

  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;

    @media (min-width: 750px) {
      flex-direction: row;
      align-items: unset;
      justify-content: unset;
    }
  }
}
</style>
