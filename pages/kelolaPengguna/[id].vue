<template>
    <div class="mt-5 container"> <!-- container: untuk menjadikan table lebih rapi -->

        <div class="card">
            <div class="card-header">
                <h4>Edit Pengguna
                    <NuxtLink to="/kelolaPengguna" class="btn btn-danger float-end">Back</NuxtLink>
                </h4>
            </div>
            <div class="card-body">

                <div v-if="isLoading"> <!-- digunakan untuk memuat loading padahal sudah benar-->
                    <Loading :title="isLoadingTitle" />
                </div>
                <div v-else>
                    <form @submit.prevent="updateKelolapengguna">
                        <div class="mb-3">
                            <label>Nama</label>
                            <input type="text"   v-model="kelolapengguna.nama" class="form-control" />
                            <!-- v-model digunakan untuk memasukkan data kelola di export default-->
                            <span class="text-danger" v-if="this.errorList.nama"> {{ this.errorList.nama[0] }}</span>
                        </div>
                        <div class="mb-3">
                            <label>Email</label>
                            <input type="text" v-model="kelolapengguna.email" class="form-control" />
                            <span class="text-danger" v-if="this.errorList.email"> {{ this.errorList.email[0] }}</span>
                        </div>
                        <div class="mb-3">
                            <label>Jabatan</label>
                            <input type="text" v-model="kelolapengguna.jabatan" class="form-control" />
                            <span class="text-danger" v-if="this.errorList.jabatan"> {{ this.errorList.jabatan[0] }}</span>
                        </div>
                        <div class="mb-3">
                            <label>Jenis Kelamin</label>
                            <input type="text" v-model="kelolapengguna.jeniskelamin" class="form-control" />
                            <span class="text-danger" v-if="this.errorList.jeniskelamin"> {{
                                this.errorList.jeniskelamin[0] }} </span>
                        </div>
                        <div class="mb-3">
                            <label>Telp</label>
                            <input type="text" v-model="kelolapengguna.telp" class="form-control" />
                            <span class="text-danger" v-if="this.errorList.telp"> {{ this.errorList.telp[0] }}</span>
                        </div>
                        <div class="mb-3">
                            <label>Kode RFID</label>
                            <input type="text" v-model="kelolapengguna.koderfid" class="form-control" />
                            <span class="text-danger" v-if="this.errorList.koderfid"> {{ this.errorList.koderfid[0]
                            }}</span>
                        </div>
                        <div class="mb-3">
                            <label>Face Recognition</label>
                            <input type="text" v-model="kelolapengguna.faceid" class="form-control" />
                            <span class="text-danger" v-if="this.errorList.faceid"> {{ this.errorList.faceid[0] }}</span>
                        </div>
                        <div class="mb-3">
                            <label>Fingerprint</label>
                            <input type="text" v-model="kelolapengguna.fingerprint" class="form-control" />
                            <span class="text-danger" v-if="this.errorList.fingerprint"> {{ this.errorList.fingerprint[0]
                            }}</span>
                        </div>
                        <div>
                            <button type="submit" class="btn btn-primary">Update</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    name: "kelolapenggunaEdit",
    data() {
        return {
            
            kelolapenggunaId: '',
            kelolapengguna: {},
            isLoading: false,
            isLoadingTitle: 'Loading',//loading digunakan untuk menampilkan loading waktu proses penginputan
            errorList: {},
            _token:'{{ csrf_token() }}'
        }
    },
    mounted() {

        this.kelolapenggunaId = this.$route.params.id
        //alert(this.kelolapenggunaId);

        this.getKelolapengguna(this.kelolapenggunaId);
    },
    methods: {

        getKelolapengguna(kelolapenggunaId) {

            this.isLoading = true;
            axios.get(`http://localhost:8000/api/kelolapengguna/${kelolapenggunaId}/editpengguna`).then(res => {

                //console.log(res);
                this.isLoading = false;
                this.kelolapengguna = res.data.kelolapengguna
            });
        },

        updateKelolapengguna() { //saveKelolapengguna untuk menyimpan di phpmyadmin

            this.isLoading = true;
            this.isLoadingTitle = "Updating";
            //alert('am here');

            var myThis = this;

            axios.put(`http://localhost:8000/api/kelolapengguna/${this.kelolapenggunaId}/updatepengguna`, this.kelolapengguna)
                .then(res => {
                    console.log(res, 'res');
                    alert(res.data.message);

                    this.isLoading = false;
                    this.isLoadingTitle = "Loading";

                    this.errorList = {};

                    // Navigasi ke halaman sebelumnya (halaman Kelola Pengguna)
                    this.$router.go(-1);
                })
                .catch(function (error) {
                    console.log(error, 'errors')

                    if (error.response) {
                        if (error.response.status == 422) {
                            myThis.errorList = error.response.data.errors;
                        }
                    }

                    myThis.isLoading = false;
                });

        }
    },
}
</script>

<style lang="scss" scoped></style>