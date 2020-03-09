<template>
  <div id="app" class="is-relative">
    <transition name="fade">
      <div v-if="filters.length" class="filter is-stack-40">
        <div class="is-stack-8 is-small">
          <strong>VALITSE MAALAUSTYÖ</strong>
        </div>
        <button
          @click.prevent="toggleFilter(filter.Name)"
          v-for="filter in filters"
          :key="filter.Id"
          :class="{ active: certificateStrings.some(e => e === filter.Name) }"
          class="button is-secondary is-small filter-button"
        >
          {{ filter.Name }}
        </button>
      </div>
    </transition>

    <div style="position: absolute;width: 100%;">
      <div v-if="!painters.length" class="fc__loader"></div>
    </div>

    <transition name="fade">
      <div class="list" v-if="painters.length">
        <painter
          v-for="painter in painters"
          :key="painter.ID"
          :painter="painter"
        />
      </div>
    </transition>
  </div>
</template>

<script>
const queryUrl =
  "https://cors-anywhere.herokuapp.com/https://tekijapankki.tikkurila.fi/sitecore/api/ssc/fpp/painters/1/";

import Painter from "./components/Painter";

export default {
  name: "App",
  data() {
    return {
      filters: [],
      painters: [],
      certificateStrings: []
    };
  },

  components: {
    Painter
  },

  watch: {
    certificateStrings() {
      this.fetchPainters();
    }
  },

  created() {
    fetch(`${queryUrl}GetCertificates?sc_lang=fi-FI&sc_site=FindPromotePainter`)
      .then(response => response.json())
      .then(data => (this.filters = data));

    this.fetchPainters();
  },

  methods: {
    toggleFilter(name) {
      let index = this.certificateStrings.findIndex(e => e === name);
      if (index > -1) {
        this.certificateStrings.splice(index, 1);
      } else {
        this.certificateStrings.push(name);
      }
    },

    fetchPainters() {
      this.painters.length = 0;

      let query = "";
      this.certificateStrings.forEach(e => {
        query = `${query}&certificateStrings=${e}`;
      });

      fetch(
        `${queryUrl}GetPaintersDynamically?Searchstring=&SortBy=desc&SortField=NumberOfProjects${query}&pageNumber=1&sc_lang=fi-FI&sc_site=FindPromotePainter`
      )
        .then(response => response.json())
        .then(data => (this.painters = data));
    }
  }
};
</script>
