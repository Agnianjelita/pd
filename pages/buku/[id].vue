<template>
  <div class="container">
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row mt-4">
      <div class="col-4">
        <img :src="buku.cover" class="cover" alt="cover buku">
      </div>
      <div class="col-md-6">
        <div class="badge bg-primary p-2">{{ buku.kategori }}</div>
        <ul class="list-group list-group-flush">
          <li class="list-group-item"><strong>penulis : </strong> {{ buku.penulis }}</li>
          <li class="list-group-item"><strong>tahun_terbit : </strong> {{ buku.tahun_terbit }}</li>
          <li class="list-group-item"><strong>pernerbit : </strong> {{ buku.penerbit  }}</li>
          <li class="list-group-item"><strong>deskripsi : </strong> {{ buku.deskripsi }}</li>
        </ul>
      </div>
    </div>
    <div class="row">
      <div class="col-lg-12 mt-5">
        <nuxt-link to="/buku/">
          <button type="submit" class="btn btn-dark rounded-3 px-5">Kembali</button>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>


<script setup>
const supabase = useSupabaseClient()
const route = useRoute()
const buku = ref([])
  
const getBookById = async () => {
  const {data, error} = await supabase
  .from('buku')
  .select(`*, kategori_buku(*)`)
  .eq('id', route.params.id)
  .single()
  if(data) buku.value = data
}

onMounted(() => {
  getBookById()
})
</script>
