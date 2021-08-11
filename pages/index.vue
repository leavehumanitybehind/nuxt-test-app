<template>
  <div class="container">
    <CreateForm />
    <Cards class="cards__wrapper"/>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>
<style lang="scss" >
.container {
  margin: 2% auto;
  max-width: 1440px;
  margin: 32px;
  @media (min-width: 768px) {
    display: flex;
    flex-direction: column;
  }

  @media (min-width: 1024px) {
    margin: 2% auto;
    flex-direction: row;
    align-items: flex-start;
    justify-content: center;
  }
}

.cards__wrapper {
  width: 100%;
}
</style>