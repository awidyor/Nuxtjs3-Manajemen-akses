<template>
       <Header /> 
     <Footer /> 
     <Sidebar /> 
  <div class="container mt-5 px-1">
    <div class="card mb-5">
      <div class="card-header">
        <h4>
          Daftar Pengguna
          <NuxtLink to="/kelolaPengguna/create" class="btn btn-primary float-end">Tambah Pengguna</NuxtLink>
        </h4>
      </div>

      <div class="card-body p-1 overflow-x-auto overflow-y-hidden mb-3">

        <div class="loading text-center" v-if="isLoading">
          <Loading title="Loading..." />
        </div>
        <div v-else>
          <table class="table table-striped table-bordered">
            <thead>
              <tr>
                <th>No. Urut</th>
                <th>Nama</th>
                <th>Email</th>
                <th>Jabatan</th>
                <th>Jenis Kelamin</th>
                <th>Telp</th>
                <th>Kode RFID</th>
                <th>Face Recognition</th>
                <th>Fingerprint</th>
                <th>Created At</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(kelolapengguna, index) in kelolapengguna" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ kelolapengguna.nama }}</td>
                <td>{{ kelolapengguna.email }}</td>
                <td>{{ kelolapengguna.jabatan }}</td>
                <td>{{ kelolapengguna.jeniskelamin }}</td>
                <td>{{ kelolapengguna.telp }}</td>
                <td>{{ kelolapengguna.koderfid }}</td>
                <td>{{ kelolapengguna.faceid }}</td>
                <td>{{ kelolapengguna.fingerprint }}</td>
                <td>{{ kelolapengguna.created_at }}</td>
                <td>
                  <NuxtLink :to="`/kelolaPengguna/${kelolapengguna.id}`" class="btn btn-primary">Edit</NuxtLink>
                  <button type="button" @click="deletekelolapengguna(kelolapengguna.id)"
                    class="btn btn-danger">Delete</button>

                </td>
              </tr>
            </tbody>
          </table>
        </div>

      </div>
    </div>
  </div>
</template>
  
<script>
import axios from 'axios';

export default {

  name: "kelolapengguna",

  data() {

    return {
      kelolapengguna: {},
      isLoading: true,
    };

  },
  mounted() {

    this.getKelolapengguna();

  },
  methods: {

    getKelolapengguna() {

      this.isLoading = true;

      axios.get('http://localhost:8000/api/kelolapengguna').then(res => {
        //console.log(res.data.kelolapengguna); // Pastikan respons sesuai dengan struktur yang diharapkan

        this.isLoading = false;
        this.kelolapengguna = res.data.kelolapengguna.map((kelolapengguna, index) => ({
            id : kelolapengguna.id,
            nomorUrut: index + 1,
            nama: kelolapengguna.nama,
            email: kelolapengguna.email,
            jabatan: kelolapengguna.jabatan,
            jeniskelamin: kelolapengguna.jeniskelamin,
            telp: kelolapengguna.telp,
            koderfid: kelolapengguna.koderfid,
            faceid: kelolapengguna.faceid,
            fingerprint: kelolapengguna.fingerprint,
            created_at: kelolapengguna.created_at,
          // Tambahkan properti nomor urut dan sembunyikan ID
          // id: pengguna.id, // Jangan sertakan ID untuk disembunyikan
        }));
      });
    },

    deletekelolapengguna(kelolapenggunaId) {

      if (confirm('Serius mau menhapus data ini??')) {
        event.target.innerText = 'Deleting';

        axios.delete(`http://localhost:8000/api/kelolapengguna/${kelolapenggunaId}/deletepengguna`).then(res => {

          event.target.innerText = 'Delete';
          this.getKelolapengguna();

        });
      }
    }
  }
}
</script>
  
<style lang="scss" scoped></style>
  