<template>
    <div class="sort__btns">
      <input v-model="search" placeholder="Поиск " />
      <button @click="sortMin">&#8593;</button>
      <button @click="sortMax">&#8595;</button>
    </div>
</template>

<script>
import { mapGetters, mapMutations } from "vuex";
export default {
  data() {
    return {
      search: "",
    };
  },
  methods: {
    ...mapMutations({
      sortMin: "cards/sortCardsMinMax",
      sortMax: "cards/sortCardsMaxMin",
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
};
</script>

<style>

</style>