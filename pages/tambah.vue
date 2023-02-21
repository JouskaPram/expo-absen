<template>
  <div class="bg-[#f2f4f6] md:h-screen">
    <div class="">
      <div class="pt-5">
        <div
          class="w-[80%] md:w-1/2 bg-[#fffffe] rounded-md shadow-sm m-auto py-7 px-5"
        >
          <h3 class="my-2 text-center font-bold text-[#00214d] text-2xl">
            Pengunjung Expo SMKN 4
          </h3>
          <form method="post" @submit.prevent="tambahAbsen">
            <label for="nama" class="font-semibold text-[#00214d] mb-2 block"
              >Nama</label
            >
            <input
              type="text"
              v-model="nama"
              class="rounded-md w-full bg-gray-50 py-3 mb-3 border border-gray-200"
            />
            <label for="alamat" class="font-semibold text-[#00214d] mb-2 block"
              >Alamat</label
            >
            <input
              type="text"
              v-model="alamat"
              class="rounded-md w-full bg-gray-50 py-3 mb-3 border border-gray-200"
            />

            <label for="pesan" class="font-semibold text-[#00214d] mb-2 block"
              >Pesan</label
            >
            <textarea
              v-model="pesan"
              id=""
              cols="30"
              rows="5"
              class="rounded-md w-full bg-gray-50 py-3 mb-3 border border-gray-200"
            ></textarea>
            <button
              type="submit"
              class="py-2 px-5 text-center text-white bg-[#00ebc7] my-2 rounded-md"
            >
              Add New
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const nama = ref();
const alamat = ref();
const email = ref();
const pesan = ref();

async function tambahAbsen() {
  const { error } = await supabase.from("absen_expo").insert({
    nama: nama.value,
    asal: alamat.value,
    email: email.value,
    pesan: pesan.value,
  });
  navigateTo("/");
}
</script>
