<template>
  <header class="header">
    <div class="container">
      <a href="#" class="menu-btn" @click="$emit('showOpen')">
        <span></span>
      </a>
      <router-link to="/" class="header__logo">
        <img width="38" src="../assets/img/pizza-logo.svg" alt="Pizza logo" />
        <div>
          <h1>
            Vue <br />
            Pizza
          </h1>
          <p>самая вкусная пицца во вселенной</p>
        </div>
      </router-link>
      <div class="header__cart">
        <router-link to="/cart" class="button button--cart">
          <span v-if="totalSum">{{ totalSum }}</span>
          <span v-else>0 ₽</span>
          <div class="button__delimiter"></div>
          <svg
            width="18"
            height="18"
            viewBox="0 0 18 18"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M6.33333 16.3333C7.06971 16.3333 7.66667 15.7364 7.66667 15C7.66667 14.2636 7.06971 13.6667 6.33333 13.6667C5.59695 13.6667 5 14.2636 5 15C5 15.7364 5.59695 16.3333 6.33333 16.3333Z"
              stroke="white"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <path
              d="M14.3333 16.3333C15.0697 16.3333 15.6667 15.7364 15.6667 15C15.6667 14.2636 15.0697 13.6667 14.3333 13.6667C13.597 13.6667 13 14.2636 13 15C13 15.7364 13.597 16.3333 14.3333 16.3333Z"
              stroke="white"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <path
              d="M4.78002 4.99999H16.3334L15.2134 10.5933C15.1524 10.9003 14.9854 11.176 14.7417 11.3722C14.4979 11.5684 14.1929 11.6727 13.88 11.6667H6.83335C6.50781 11.6694 6.1925 11.553 5.94689 11.3393C5.70128 11.1256 5.54233 10.8295 5.50002 10.5067L4.48669 2.82666C4.44466 2.50615 4.28764 2.21182 4.04482 1.99844C3.80201 1.78505 3.48994 1.66715 3.16669 1.66666H1.66669"
              stroke="white"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
          <span v-if="totalCount">{{ totalCount }}</span>
          <span v-else>0</span>
        </router-link>
      </div>
      <p v-if="itemSize">jony</p>
    </div>
  </header>
</template>

<script>
import { computed, ref } from '@vue/reactivity'
import { useStore } from 'vuex'

export default {
  setup() {
    const store = useStore()

    const totalCount = computed(() => store.getters.getAddedPizzasCount)
    const totalSum = computed(() => store.getters.getAddedPizzaSum)

    return { totalCount, totalSum }
  },
  data() {
    return {
      itemSize: false,
    }
  },
  methods: {},
}
</script>

<style lang="scss">
@import '@/assets/scss/app.scss';

.header {
  border-bottom: 1px solid $gray-line;
  padding: 40px 0;

  .container {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__logo {
    display: flex;

    img {
      margin-right: 15px;
    }

    h1 {
      color: #181818;
      font-size: 24px;
      letter-spacing: 1%;
      text-transform: uppercase;
      font-weight: 800;
    }

    br {
      display: none;
    }

    p {
      color: #7b7b7b;
    }
  }
  .menu-btn {
    display: block;
    width: 50px;
    height: 50px;
    background-color: #fe5f1e;
    border-radius: 50%;
    position: relative;
    cursor: pointer;
    span {
      position: absolute;
      top: 50%;
      margin-top: -1px;
      left: 50%;
      margin-left: -10px;
      width: 20px;
      height: 2px;
      background-color: #fff;
      &::before,
      &::after {
        content: '';
        position: absolute;
        transform: translateY(-5px);
        width: 100%;
        height: 100%;
        background-color: inherit;
      }
      &::after {
        transform: translateY(5px);
      }
    }
  }
}

@media (max-width: 799px) {
  .header {
    &__logo {
      align-items: center;
      h1 {
        font-size: 16px;
      }
      p {
        display: none;
      }
    }
  }
}

@media (max-width: 570px) {
  .header {
    &__logo {
      br {
        display: block;
      }
    }
    .menu-btn:nth-child(1) {
      order: 3;
      margin-left: 8px;
    }
  }
}
</style>
