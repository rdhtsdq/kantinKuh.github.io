<template>
  <div class="container">
    <div class="grid grid-cols-2 gap-3 p-5 bg-base-100 rounded-lg shadow">
      <div class="form-control w-full max-w-xs">
        <label class="label">
          <span class="label-text">Nama Makanan : </span>
        </label>
        <input
          type="text"
          v-model="produk.nama"
          placeholder="Type here"
          class="input input-bordered w-full max-w-xs"
        />
      </div>
      <div class="form-control w-full max-w-xs">
        <label class="label">
          <span class="label-text">Harga :</span>
        </label>
        <input
          type="text"
          v-model="produk.harga"
          placeholder="Type here"
          class="input input-bordered w-full max-w-xs"
        />
      </div>
      <div class="form-control w-full max-w-xs">
<label class="label">
          <span class="label-text">Status :</span>
        </label>
        <label class="label cursor-pointer flex justify-center">
          <div class="grid grid-cols-1 justify-items-center mx-3">
            <input
            v-model="produk.status"
            type="radio"
            name="radio-6"
            value="habis"
            class="radio checked:bg-error"
          />
          <span class="label-text font-medium">Habis</span>
        </div>
        <div class="grid grid-cols-1 justify-items-center mx-3">
          <input
            v-model="produk.status"
            type="radio"
            name="radio-6"
            value="ada"
            class="radio checked:bg-success"
          />
 <span class="label-text font-medium">Ada</span>
        </div>
        </label>
      </div>
      <div class="form-control w-full max-w-xs">
        <label class="label">
          <span class="label-text">Kategori : </span> </label
        ><select
          v-model="produk.kategori"
          class="select select-success w-full max-w-xs"
        >
          <option disabled selected>Kategori</option>
          <option>food</option>
          <option>drink</option>
          <option>snack</option>
        </select>
      </div>
      <div class="col-span-2">
        <label class="block text-sm font-medium text-gray-700">
          Cover photo
        </label>
        <div
          class="
            mt-1
            flex
            justify-center
            px-6
            pt-5
            pb-6
            border-2 border-gray-300 border-dashed
            rounded-md
          "
        >
          <div class="space-y-1 text-center">
            <img
              :src="'http://192.168.212.105:8000/storage/image/' + preview"
              alt="imagePreview"
              width="400"
            />
          </div>
        </div>
      </div>
      <div class="col-start-2 flex justify-end mt-3">
        <button @click="editProduk" class="btn btn-outline-primary">
          Edit
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from "vue";
import { useRouter, useRoute } from "vue-router";
import DataService from "../../services/DataService";
import { useKeranjangStore } from "../../stores/keranjang";
import { useProdukStore } from "../../stores/produk";

const keranjangStore = new useKeranjangStore();
const produkStore = new useProdukStore();
const router = useRouter();
const route = useRoute();

const produk = reactive({});
const isGambar = ref("");
const preview = ref("");
const produk_id = produkStore.produkId;

produk.nama = produk_id.nama;
produk.harga = produk_id.harga;
produk.kategori = produk_id.nama;
produk.kode = produk_id.kode;
produk.status = produk_id.status;
produk.gambar = produk_id.gambar
preview.value = produk_id.gambar;

//

const getImage = (event) => {
  isGambar.value = event.target.files[0];
  console.log(isGambar);
  console.log(event.target.files[0]);
  preview.value = URL.createObjectURL(event.target.files[0]);
  keranjangStore.codeGenerator(5);
};

const editProduk = async () => {
  const formData = new FormData();
  formData.append("nama", produk.nama);
  formData.append("harga", produk.harga);
  formData.append("kategori", produk.kategori);
  formData.append("kode", produk.kode);
  formData.append("status", produk.status);
  if (isGambar.value != "") {
    console.log(isGambar);
    formData.append("gambar", isGambar);
  }
  try {
    if (isGambar.value != "") {
      await DataService.editProduk(produk.kode, produk, {
        headers: {
          "Content-Type": "multipart/form-data",
        },
      });
    } else {
      await DataService.editProduk(produk.kode, produk);
    }
    router.push({ name: "Produk" });
    console.log(isGambar);
  } catch (err) {
    console.log(err);
  }
};
</script>
