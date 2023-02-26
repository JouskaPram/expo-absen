<template>
  <div class="isolate bg-white px-6 sm:py-32 lg:px-8 text-left">
    <div
      class="fixed top-0 right-0 mt-4 mr-4 text-white py-2 px-4 rounded-md"
      v-if="datas.length > 0"
    >
      <div
        class="mb-3 w-full rounded-lg bg-success-100 py-5 px-6 text-base text-success-700 flex justify-between items-center"
      >
        <div
          v-for="(alert, index) in datas"
          :key="index"
          class=""
          :class="'alert-' + alert.type"
        >
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <svg
                class="h-5 w-5 text-green-400"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path
                  fill-rule="evenodd"
                  d="M18.707,3.293c-0.391,-0.391 -1.023,-0.391 -1.414,0L9,11.586L4.707,7.293c-0.391,-0.391 -1.023,-0.391 -1.414,0c-0.391,0.391 -0.391,1.023 0,1.414l5,5c0.195,0.195 0.451,0.293 0.707,0.293s0.512,-0.098 0.707,-0.293l9,-9c0.391,-0.391 0.391,-1.023 0,-1.414Z"
                />
              </svg>
            </div>
            <div class="ml-3">
              <p class="text-sm font-medium">{{ alert.message }}</p>
            </div>
          </div>
          <!-- <button
            
            type="button"
            class="ml-3 bg-transparent text-3xl rounded-lg bg-success-100"
            data-bs-dismiss="alert"
            @click="datas.splice(index, 1)"
          >
            &times;
          </button> -->
        </div>
      </div>
    </div>

    <div
      class="absolute inset-x-0 top-[-10rem] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[-20rem]"
    >
      <img
        src="@/assets/img/logo.png"
        alt="gambar"
        class="relative left-1/2 -z-10 h-[21.1875rem] max-w-none -translate-x-1/2 rotate-[30deg] sm:left-[calc(50%-40rem)] sm:h-[42.375rem] opacity-70"
      />
    </div>
    <div class="mx-auto max-w-2xl text-center">
      <h2
        class="font-extrabold text-5xl sm:text-4xl text-gradient-to-r from-blue-500 to-gray-900"
      >
        EXPO 2023
      </h2>
      <p class="mt-2 text-lg leading-8 text-gray-600">
        Selamat datang di buku tamu SMKN 4
      </p>
    </div>
    <form
      @submit.prevent="tambahAbsen"
      method="POST"
      class="mx-auto mt-5 max-w-xl sm:mt-5"
    >
      <div class="grid grid-cols-2 gap-y-6 gap-x-8">
        <div class="col-span-1">
          <label
            for="first-name"
            class="block text-sm font-semibold leading-6 text-gray-900"
            >Nama</label
          >
          <div class="mt-2.5">
            <input
              type="text"
              name="first-name"
              id="first-name"
              autocomplete="given-name"
              required
              v-model="nama"
              class="block w-full rounded-md border-0 py-2 px-3.5 text-sm leading-6 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600"
            />
          </div>
        </div>
        <div class="col-span-1">
          <label
            for="last-name"
            class="block text-sm font-semibold leading-6 text-gray-900"
            >Instansi/Sekolah</label
          >
          <div class="mt-2.5">
            <input
              type="text"
              name="last-name"
              id="last-name"
              required
              autocomplete="family-name"
              v-model="alamat"
              class="block w-full rounded-md border-0 py-2 px-3.5 text-sm leading-6 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600"
            />
          </div>
        </div>

        <div class="col-span-2">
          <label
            for="message"
            class="block text-sm font-semibold leading-6 text-gray-900"
            >Pesan/Kesan</label
          >
          <div class="mt-2.5">
            <textarea
              name="message"
              id="message"
              required
              rows="4"
              v-model="pesan"
              class="block w-full rounded-md border-0 py-2 px-3.5 text-sm leading-6 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600"
            ></textarea>
          </div>
        </div>
      </div>
      <div class="mt-10">
        <button
          type="submit"
          class="block w-full rounded-md bg-sky-500 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          Masukan
        </button>
      </div>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const nama = ref();
const alamat = ref();
const email = ref();
const pesan = ref();
const datas = ref([]);

async function tambahAbsen() {
  const { error } = await supabase.from("absen_expo").insert({
    nama: nama.value,
    asal: alamat.value,

    pesan: pesan.value,
  });
  if (error) {
    console.error(error);
  } else {
    const alert = {
      message: "sukses di tambahkan",
    };
    datas.value.push(alert);
  }
  nama.value = "";
  alamat.value = "";
  pesan.value = "";
}
definePageMeta({
  middleware: "auth",
});
</script>
