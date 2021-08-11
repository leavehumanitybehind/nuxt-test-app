<template>
  <form class="form" @submit.prevent="submitData">
    <div class="form__row">
      <label> Наименование товара* </label>
      <input
        :class="{ errorStyle: $v.name.$error }"
        v-model="name"
        placeholder="Наименование товара"
      />
    </div>
    <div class="form__row">
      <label> Описание товара </label>
      <textarea
        v-model="desc"
        placeholder="Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"
      >
      </textarea>
    </div>
    <div class="form__row">
      <label> Ссылка* </label>
      <input
        :class="{ errorStyle: $v.imgLink.$error }"
        v-model="imgLink"
        type="text"
        placeholder="https://google.com/image.jpg"
      />
    </div>
    <div class="form__row">
      <label> Цена товара* </label>
      <input
        :class="{ errorStyle: $v.price.$error }"
        v-model="price"
        placeholder="12 000"
        type="number"
      />
    </div>
    <button type="submit" :disabled="$v.$invalid" class="form__btn">
      Добавить товар
    </button>
  </form>
</template>

<script>
import Vue from "vue";
import Vuelidate from "vuelidate";
import { required } from "vuelidate/lib/validators";
Vue.use(Vuelidate);
export default {
  data() {
    return {
      name: "",
      desc: "",
      imgLink: "",
      price: "",
    };
  },
  validations: {
    name: {
      required,
    },
    imgLink: {
      required,
    },
    price: {
      required,
    },
  },
  methods: {
    resetField() {
      this.name = "";
      this.desc = "";
      this.imgLink = "";
      this.price = "";
    },
    submitData() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      } else {
        this.$store.commit("cards/addCard", {
          title: this.name,
          description: this.desc,
          img: this.imgLink,
          price: this.price,
        });

        this.resetField();
      }
    },
  },
};
</script>

<style lang="scss">
.form {
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding: 24px;
  text-align: left;

  @media (min-width: 1124px) {
    position: sticky;
    top: 5%;
    margin: 0 16px;
    margin-right: 16px;
  }
}

.form__row {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
}
.form__row label {
  font-size: 0.625rem;
  line-height: 13px;
  letter-spacing: -0.02em;
}

.form__btn {
  width: 100%;
  padding: 10px 0;
  font-family: Inter;
  font-style: normal;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  background: #7bae73;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  color: white;
  border: none;
  cursor: pointer;

  &:disabled {
    background-color: rgb(78, 77, 77);
    cursor: no-drop;
  }

  &:hover,
  &:focus {
    background: #a2bb9e;
  }
}

input,
textarea {
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  padding: 10px 16px;
  outline: none;
  font-size: 16px;

  &:hover,
  &:focus {
    outline: 1px solid rgb(108, 108, 230);
  }
}

textarea {
  height: 108px;
}

@media (min-width: 1124px) {
  input,
  textarea {
    width: 250px;
  }
}

.errorStyle {
  outline: 1px solid red;
  -webkit-animation: shake 0.6s;
  animation: shake 0.6s;
}

@-webkit-keyframes bounce {
  0% {
    -webkit-transform: translateY(-100px);
    transform: translateY(-100px);
  }

  70% {
    -webkit-transform: translateY(30px);
    transform: translateY(30px);
  }

  90% {
    -webkit-transform: translateY(-10px);
    transform: translateY(-10px);
  }

  100% {
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
}

@keyframes bounce {
  0% {
    -webkit-transform: translateY(-100px);
    transform: translateY(-100px);
  }

  70% {
    -webkit-transform: translateY(30px);
    transform: translateY(30px);
  }

  90% {
    -webkit-transform: translateY(-10px);
    transform: translateY(-10px);
  }

  100% {
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
}

@-webkit-keyframes shake {
  0%,
  100% {
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }

  10%,
  30%,
  50%,
  70%,
  90% {
    -webkit-transform: translateX(-10px);
    transform: translateX(-10px);
  }

  20%,
  40%,
  60%,
  80% {
    -webkit-transform: translateX(10px);
    transform: translateX(10px);
  }
}

@keyframes shake {
  0%,
  100% {
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }

  10%,
  30%,
  50%,
  70%,
  90% {
    -webkit-transform: translateX(-10px);
    transform: translateX(-10px);
  }

  20%,
  40%,
  60%,
  80% {
    -webkit-transform: translateX(10px);
    transform: translateX(10px);
  }
}
</style>