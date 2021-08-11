<template>
  <div>
    <SortForm v-model="search" />
    <Loader v-if="!init" />
    <div v-else class="cards">
      <div v-for="(card, index) in filteredList" :key="index">
        <Card :item="card" />
      </div>
    </div>
  </div>
</template>
<script>
import { mapGetters, mapMutations } from "vuex";
export default {
  data() {
    return {
      search: "",
      init: false,
    };
  },
  methods: {
    ...mapMutations({
      setLocalStorage: "cards/setDataFromLocalStorage",
    }),
  },
  computed: {
    ...mapGetters({
      cards: "cards/getCards",
    }),
    filteredList() {
      let comp = this.search.toLowerCase();
      return this.cards.filter(
        (elem) => elem.title.toLowerCase().indexOf(comp) > -1
      );
    },
  },
  mounted() {
    setTimeout(() => {
      localStorage.cards ? this.setLocalStorage() : "";
      this.init = true;
    }, 1500);
  },
};
</script>
<style lang="scss" scoped>
.cards {
  justify-content: center;
  @media (min-width: 768px) {
    display: grid;
    grid-template-columns: repeat(2, 332px);
    grid-auto-rows: 1fr;
    grid-column-gap: 30px;
    grid-row-gap: 30px;
  }

  @media (min-width: 1124px) {
    grid-template-columns: repeat(3, 332px);
  }
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to {
  opacity: 0;
}
</style>

