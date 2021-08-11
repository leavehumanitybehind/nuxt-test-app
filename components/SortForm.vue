<template>
  <div class="sort__btns">
    <input :value="search" @input="$emit('input', $event.target.value)" placeholder="Поиск " />
    <button @click="sortMin">&#8593;</button>
    <button @click="sortMax">&#8595;</button>
  </div>
</template>
<script>
import { mapMutations } from "vuex";
export default {
  props: ["search"],
  data() {
    return {

    };
  },
  methods: {
    ...mapMutations({
      sortMin: "cards/sortCardsMinMax",
      sortMax: "cards/sortCardsMaxMin",
    }),
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
</style>

