<script setup>
const supabase = useSupabaseAuthClient();
const datas = ref([]);
const loading = ref(true);
async function getAbsen() {
  loading.value = true;
  const { data, error } = await supabase
    .from("absen_expo")
    .select()
    .order("id", { ascending: false });
  datas.value = data;
  loading.value = false;
}
async function signOut() {
  const { error } = await supabase.auth.signOut();
}
onMounted(() => {
  getAbsen();
});
</script>
<template>
  <div class="bg-[#f2f4f6] md:h-screen">
    <div class="container">
      <div class="grid grid-cols-4 gap-6 pt-10">
        <div class="col-span-4">
          <div
            class="w-full rounded-md bg-[#fffffe] shadow-sm px-10 py-10 flex flex-wrap align-middle items-center"
          >
            <img
              src="@/assets/img/logo.png"
              alt=""
              srcset=""
              class="w-32 h-32 flex"
            />
            <div class="mx-5">
              <h3 class="font-extrabold text-2xl text-[#]">
                Buku Absen • EXPO <span class="text-sky-500">2023</span>
              </h3>
              <h3 class="text-left font-bold text-[#00214d] text-2xl">
                SMKN 4 Tasimalaya
              </h3>

              <p class="text-left font-semibold text-[#1b2d45]">
                Jl.Depo No.31
              </p>
            </div>
            <div
              class="w-36 h-32 ml-auto bg-sky-500 rounded-md shadow-sm text-center flex justify-center items-center align-middle"
            >
              <div class="p-3">
                <div v-if="datas.length < 1" class="mb-5 text-xl text-white">
                  <em>loading..</em>
                </div>
                <div
                  v-else
                  class="font-bold font-mono text-white text-4xl block"
                >
                  {{ datas.length }}
                  <span class="text-2xl">Pengunjung</span>
                </div>
              </div>
            </div>
          </div>
          <!-- table section -->
          <div class="w-full bg-[#fffffe] shadow-sm px-10 py-5 rounded-md mt-5">
            <div class="container">
              <h3 class="text-[#00214d] font-bold text-xl my-3">
                Pengunjung Expo
                <span class="text-sky-500 font-extrabold">2023</span>
              </h3>
              <table class="m-auto table border-collapse w-full">
                <td
                  v-if="loading"
                  colspan="4"
                  class="py-3 text-slate-900 text-sm text-center"
                >
                  <em>sedang memuat...</em>
                </td>
                <thead class="bg-sky-500 rounded-l-md rounded-r-md">
                  <tr>
                    <th
                      class="text-gray-100 border-gray-200 py-2 px-4 rounded-tl-md"
                    >
                      No
                    </th>
                    <th
                      class="text-gray-100 border-gray-200 py-2 px-4 whitespace-nowrap"
                    >
                      Nama
                    </th>
                    <th class="text-gray-100 border-gray-200 py-2 px-4">
                      Instansi
                    </th>
                    <th
                      class="text-gray-100 border-gray-200 py-2 px-4 rounded-tr-md"
                    >
                      Pesan
                    </th>
                  </tr>
                </thead>
                <tbody class="">
                  <tr v-for="(data, i) in datas" :key="data.id">
                    <td
                      class="text-center text-[#1b2d45] font-medium px-2 border-l border-r border-b border-gray-100 py-2"
                    >
                      {{ i + 1 }}
                    </td>
                    <td
                      class="text-left text-[#1b2d45] font-medium whitespace-nowrap px-2 border-r border-b border-gray-100 py-2"
                    >
                      {{ data.nama }}
                    </td>
                    <td
                      class="text-left text-[#1b2d45] font-medium px-2 border-r border-b border-gray-100 py-2"
                    >
                      {{ data.asal }}
                    </td>
                    <td
                      class="text-left text-[#1b2d45] font-medium px-2 border-r border-b border-gray-100 py-2"
                    >
                      {{ data.pesan }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>

      <!-- info section -->
    </div>
  </div>
</template>
<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins&display=swap");
.container {
  font-family: "Poppins", sans-serif;
}
</style>
