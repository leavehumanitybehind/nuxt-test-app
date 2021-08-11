<template>
  <div>
    <div class="sort__btns">
      <input v-model="search" placeholder="Поиск " />
      <button @click="sortMin">&#8593;</button>
      <button @click="sortMax">&#8595;</button>
    </div>
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
      sortMin: "cards/sortCardsMinMax",
      sortMax: "cards/sortCardsMaxMin",
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
.sort__btns {
  display: flex;
  justify-content: flex-start;
  margin: 40px 0;

  @media (min-width: 1068px) {
    margin: 10px 0 30px;
  }

  & input {
    width: 100%;

    @media (min-width: 1068px) {
      width: auto;
    }

    &:hover,
    &:focus {
      outline: 1px solid rgb(108, 108, 230);
    }
  }
}

.cards {
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

