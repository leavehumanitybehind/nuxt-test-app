<template>
  <div>
    <div class="sort__btns">
      <input v-model="search" placeholder="Поиск " />
      <button @click="sortMin">&#8593;</button>
      <button @click="sortMax">&#8595;</button>
    </div>
    <div class="loader" v-if="!init"> 
        <svg class="circular" viewBox="25 25 50 50">
    <circle class="path" cx="50" cy="50" r="20" fill="none" stroke-width="2" stroke-miterlimit="10"/>
  </svg> </div>
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
    setTimeout(()=> {
      localStorage.cards ? this.setLocalStorage() : "";
      this.init = true;
      
    }, 2000)
    
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

.loader {
  position: relative;
  margin: 5% auto;
  width: 100px;
}

.loader:before {
  content: '';
  display: block;
  padding-top: 100%;
}

.circular {
  -webkit-animation: rotate 2s linear infinite;
  animation: rotate 2s linear infinite;
  height: 100%;
  -webkit-transform-origin: center center;
  -ms-transform-origin: center center;
  transform-origin: center center;
  width: 100%;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}

.path {
  stroke-dasharray: 1, 200;
  stroke-dashoffset: 0;
  -webkit-animation: dash 1.5s ease-in-out infinite, color 6s ease-in-out infinite;
  animation: dash 1.5s ease-in-out infinite, color 6s ease-in-out infinite;
  stroke-linecap: round;
}

@-webkit-keyframes 
rotate {  100% {
 -webkit-transform: rotate(360deg);
 transform: rotate(360deg);
}
}

@keyframes 
rotate {  100% {
 -webkit-transform: rotate(360deg);
 transform: rotate(360deg);
}
}

@-webkit-keyframes 
dash {  0% {
 stroke-dasharray: 1, 200;
 stroke-dashoffset: 0;
}
 50% {
 stroke-dasharray: 89, 200;
 stroke-dashoffset: -35;
}
 100% {
 stroke-dasharray: 89, 200;
 stroke-dashoffset: -124;
}
}

@keyframes 
dash {  0% {
 stroke-dasharray: 1, 200;
 stroke-dashoffset: 0;
}
 50% {
 stroke-dasharray: 89, 200;
 stroke-dashoffset: -35;
}
 100% {
 stroke-dasharray: 89, 200;
 stroke-dashoffset: -124;
}
}

@-webkit-keyframes 
color {  100%, 0% {
 stroke: #d62d20;
}
 40% {
 stroke: #0057e7;
}
 66% {
 stroke: #008744;
}
 80%, 90% {
 stroke: #ffa700;
}
}

@keyframes 
color {  100%, 0% {
 stroke: #d62d20;
}
 40% {
 stroke: #0057e7;
}
 66% {
 stroke: #008744;
}
 80%, 90% {
 stroke: #ffa700;
}
}
</style>

