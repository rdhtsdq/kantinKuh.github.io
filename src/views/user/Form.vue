<template>
  <!-- component -->
  <div class="h-screen md:flex">
    <div
      class="
        relative
        overflow-hidden
        md:flex
        w-1/2
        bg-gradient-to-tr
        from-emerald-500
        to-green-400
        i
        justify-around
        items-center
        hidden
      "
    >
      <div>
        <h1 class="text-white font-bold text-4xl font-sans">KantinKuh</h1>
        <p class="text-white mt-1">The most popular app for ordering food</p>
      </div>
      <div
        class="
          absolute
          -bottom-32
          -left-40
          w-80
          h-80
          border-4
          rounded-full
          border-opacity-30 border-t-8
        "
      ></div>
      <div
        class="
          absolute
          -bottom-40
          -left-20
          w-80
          h-80
          border-4
          rounded-full
          border-opacity-30 border-t-8
        "
      ></div>
      <div
        class="
          absolute
          -top-40
          -right-0
          w-80
          h-80
          border-4
          rounded-full
          border-opacity-30 border-t-8
        "
      ></div>
      <div
        class="
          absolute
          -top-20
          -right-20
          w-80
          h-80
          border-4
          rounded-full
          border-opacity-30 border-t-8
        "
      ></div>
    </div>
    <div class="flex md:w-1/2 justify-center py-10 items-center bg-white">
      <div
        class="
          card
          flex-shrink-0
          w-full
          max-w-sm
          md:shadow-2xl
          sm:shadow-none
          bg-base-100
        "
      >
        <div class="card-body">
          <h1 class="text-gray-800 font-bold text-2xl mb-7">
            Welcome Back Again!
          </h1>

          <!-- <div class="form-control">
            <label class="label">
              <span class="label-text">No Meja</span>
            </label>
            <input
              type="text"
              placeholder="no meja"
              v-model="dataUser.meja"
              class="input input-bordered"
            />
          </div>-->
          <div class="form-control">
            <label class="label">
              <span class="label-text">Nama</span>
            </label>
            <input
              type="text"
              placeholder="nama"
              v-model="dataUser.nama"
              class="input input-bordered"
            />
          </div>

          <div class="form-control">
            <label class="label">
              <span class="label-text">Telepon</span>
            </label>
            <input
              type="text"
              placeholder="nama"
              v-model="dataUser.telepon"
              class="input input-bordered"
            />
          </div>
          <div class="form-control mt-6">
            <button
              class="btn btn-success"
              @click="login"
              :class="{ loading: isLoading }"
            >
              Login
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref, onMounted } from "vue";
import { useLoginGuard } from "../../stores/loginGuard.js";
import { useRouter, useRoute } from "vue-router";
import { useTransaksiStore } from "../../stores/transaksi.js";
//import CryptoJS from "crypto-js";

const useTransaksi = useTransaksiStore();
const router = useRouter();
const route = useRoute();
const loginGuard = useLoginGuard();

const user = reactive({});
const isLoading = ref(false);
const dataUser = reactive({});
const secretKey = "123#$%";

onMounted(() => {
  // get data from params
  dataUser.meja = route.params.id;
  console.log(dataUser.meja);

  // decrypt data and convert to string
  //const decryptData = CryptoJS.AES.decrypt(meja, secretKey).toString(
  //CryptoJS.enc.Utf8
  //);
  //console.log(decryptData);
});

const login = () => {
  isLoading.value = true;
  useTransaksi.setUser(dataUser);
  router.push({ name: "UserHome" });
};
</script>
