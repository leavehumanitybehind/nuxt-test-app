<template>
  <div class="card" :class="{ hide: hidden }" :key="item.title">
    <button class="card__btn" @click="deleteI(item)">
      <svg
        width="16"
        height="16"
        viewBox="0 0 16 16"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g clip-path="url(#clip0)">
          <path
            d="M10.207 5.79681C10 5.79681 9.83228 5.96455 9.83228 6.17152V13.2535C9.83228 13.4603 10 13.6282 10.207 13.6282C10.4139 13.6282 10.5817 13.4603 10.5817 13.2535V6.17152C10.5817 5.96455 10.4139 5.79681 10.207 5.79681Z"
            fill="white"
          />
          <path
            d="M5.78535 5.79681C5.57838 5.79681 5.41064 5.96455 5.41064 6.17152V13.2535C5.41064 13.4603 5.57838 13.6282 5.78535 13.6282C5.99232 13.6282 6.16006 13.4603 6.16006 13.2535V6.17152C6.16006 5.96455 5.99232 5.79681 5.78535 5.79681Z"
            fill="white"
          />
          <path
            d="M2.56301 4.76329V13.9953C2.56301 14.5409 2.76309 15.0534 3.11262 15.421C3.46054 15.7898 3.94473 15.9991 4.45147 15.9999H11.541C12.0479 15.9991 12.5321 15.7898 12.8799 15.421C13.2294 15.0534 13.4295 14.5409 13.4295 13.9953V4.76329C14.1243 4.57887 14.5745 3.90762 14.4816 3.19465C14.3885 2.48183 13.7812 1.94861 13.0622 1.94846H11.1438V1.48008C11.146 1.0862 10.9902 0.707978 10.7114 0.429729C10.4326 0.151627 10.0538 -0.00323193 9.65988 -1.18018e-05H6.33261C5.93873 -0.00323193 5.55992 0.151627 5.28109 0.429729C5.00225 0.707978 4.84652 1.0862 4.84871 1.48008V1.94846H2.93025C2.21128 1.94861 1.60399 2.48183 1.5109 3.19465C1.41796 3.90762 1.86819 4.57887 2.56301 4.76329ZM11.541 15.2505H4.45147C3.81081 15.2505 3.31242 14.7002 3.31242 13.9953V4.79623H12.6801V13.9953C12.6801 14.7002 12.1817 15.2505 11.541 15.2505ZM5.59812 1.48008C5.59564 1.28497 5.67233 1.09717 5.8108 0.959441C5.94912 0.821707 6.13735 0.746034 6.33261 0.7494H9.65988C9.85514 0.746034 10.0434 0.821707 10.1817 0.959441C10.3202 1.09703 10.3969 1.28497 10.3944 1.48008V1.94846H5.59812V1.48008ZM2.93025 2.69787H13.0622C13.4348 2.69787 13.7367 2.99983 13.7367 3.37234C13.7367 3.74485 13.4348 4.04681 13.0622 4.04681H2.93025C2.55774 4.04681 2.25578 3.74485 2.25578 3.37234C2.25578 2.99983 2.55774 2.69787 2.93025 2.69787Z"
            fill="white"
          />
          <path
            d="M7.99629 5.79681C7.78932 5.79681 7.62158 5.96455 7.62158 6.17152V13.2535C7.62158 13.4603 7.78932 13.6282 7.99629 13.6282C8.20326 13.6282 8.371 13.4603 8.371 13.2535V6.17152C8.371 5.96455 8.20326 5.79681 7.99629 5.79681Z"
            fill="white"
          />
        </g>
        <defs>
          <clipPath id="clip0">
            <rect width="16" height="16" fill="white" />
          </clipPath>
        </defs>
      </svg>
    </button>
    <img :src="item.img" width="332" height="200" />
    <div class="card__text">
      <h3>{{ item.title }}</h3>
      <p>{{ item.description }}</p>
      <h5>{{ format(item.price) }} руб.</h5>
    </div>
  </div>
</template>

<script>
import { mapMutations } from "vuex";
export default {
  props: ["item"],
  data() {
    return {
      hidden: false,
    };
  },
  methods: {
    ...mapMutations({
      deleteItem: "cards/deleteCard",
    }),
    deleteI(item) {
      this.hidden = true;
      setTimeout(() => {
        this.deleteItem(item);
        this.hidden = false;
      }, 2000);
    },
    format: function (num) {
      return num
        .toString()
        .split(/(?=(?:\d{3})+(?:\.|$))/g)
        .join(" ");
    },
  },
};
</script>

<style lang='scss'>
.card {
  background-color: white;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  position: relative;
  height: 100%;
  margin-bottom: 30px;
  transition: opacity 1.5s ease-in-out;

  &__text {
    padding: 5px;
  }

  & img {
    width: 100%;
  }

  & .text {
    padding: 16px;
  }

  &__btn {
    position: absolute;
    top: -2%;
    right: -2%;
    transition: opacity 0.5s ease-out;
    opacity: 0;
    background: #ff8484;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    border: none;
    width: 32px;
    height: 32px;
    cursor: pointer;
    text-align: center;
  }
  &:hover .card__btn {
    opacity: 1;
  }
}

.hide {
  opacity: 0;
}
</style>