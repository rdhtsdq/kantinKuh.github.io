<template>
  <div>
    <div class="navbar bg-base-100 sm:shadow sm:rounded-box fixed z-30 rounded-b-lg">
      <div class="navbar-start">
        <h1 class="sm:hidden font-medium text-2xl ml-3">KantinKuh</h1>
        <div
          class="dropdown sm:block hidden"
          :class="{ 'dropdown-open': isDropdown }"
        >
          <label
            class="btn btn-ghost btn-circle"
            @click="isDropdown = !isDropdown"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h7"
              />
            </svg>
          </label>
          <ul
            tabindex="0"
            class="
              menu menu-compact
              dropdown-content
              mt-3
              p-2
              shadow
              bg-base-100
              rounded-box
              w-52
            "
          >
            <li>
              <router-link class="active:bg-success" to="/user"
                >Home</router-link
              >
            </li>
            <li>
              <router-link class="active:bg-success" to="/user/menu"
                >Menu</router-link
              >
            </li>
            <li>
              <router-link class="active:bg-success" to="/user/transaksi"
                >Pesanan</router-link
              >
            </li>
          </ul>
        </div>
      </div>
      <div class="navbar-center">
        <h1 class="normal-case text-xl hidden sm:block">KantinKuh</h1>
      </div>
      <div class="navbar-end">
        <router-link
          to="/user/keranjang"
          tabindex="0"
          class="btn btn-ghost btn-circle bg-base-100 sm:flex hidden"
        >
          <div class="indicator">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
              />
            </svg>
            <span
              class="badge badge-xs indicator-item"
              v-if="keranjangLength.value !== 0"
              >{{ keranjangLength }}</span
            >
          </div>
        </router-link>
      </div>
    </div>

    <!-- Mobile -->
    <ul
      class="
        menu menu-horizontal
        bg-base-200
        fixed
        flex
        sm:hidden
        justify-around
        inset-x-0
        bottom-0
        md:hidden
        z-20
      "
    >
      <li>
        <router-link to="/user" class="rounded-lg m-2 p-2">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-7 w-7"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"
            />
          </svg>
        </router-link>
      </li>
      <li>
        <router-link to="/user/menu" class="rounded-lg m-2 p-2">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-7 w-7"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
            />
          </svg>
        </router-link>
      </li>
      <li>
        <router-link to="/user/transaksi" class="rounded-lg m-2 p-2">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-7 w-7"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"
            />
          </svg>
        </router-link>
      </li>
      <li>
        <router-link to="/user/keranjang" class="rounded-lg m-2 p-2">
          <div class="indicator">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-7 w-7"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
              />
            </svg>
            <span
              class="badge badge-xs indicator-item"
              v-if="keranjangLength !== 0"
              >{{ keranjangLength }}</span
            >
          </div>
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import { useKeranjangStore } from "../../stores/keranjang.js";
import { useTransaksiStore } from "../../stores/transaksi.js";

export default {
  setup() {
    const keranjangStore = useKeranjangStore();
    const transaksiStore = useTransaksiStore();

    const keranjangLength = ref("0");
    const isDropdown = ref(false);

    onMounted(() => {
      transaksiStore.getUser();
    });

    if (localStorage.keranjang !== null) {
      keranjangStore.$subscribe(
        (mutation, state) => {
          keranjangLength.value = state.keranjangLength;
        },
        { detached: true }
      );
    } else if (localStorage.keranjang == nul) {
      keranjangLength.value = 0;
    }

    return { keranjangLength, isDropdown };
  },
};
</script>
