<template>
    <div class="mt-5 mb-5 container"> <!-- container: untuk menjadikan table lebih rapi -->

        <div class="card">
            <div class="card-header">
                <h4>Tambah Pengguna
                    <NuxtLink to="/kelolaPengguna" class="btn btn-danger float-end">Back</NuxtLink>
                </h4>
            </div>
            <div class="card-body">

                <div v-if="isLoading"> <!-- digunakan untuk memuat loading padahal sudah benar-->
                    <Loading :title="isLoadingTitle" />
                </div>
                <div v-else>
                    <form @submit.prevent="savekelolapengguna">

                        <div class="mb-3">
                            <label>Nama</label>
                            <input type="text" v-model="kelolapengguna.nama" class="form-control" />
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
                            <select v-model="kelolapengguna.jabatan" class="form-control">
                                <option value="" disabled>Pilih Jabatan</option>
                                <option v-for="option in jabatanOptions" :key="option.value" :value="option.value">
                                    {{ option.label }}
                                </option>
                            </select>
                            <span class="text-danger" v-if="this.errorList.jabatan">{{ this.errorList.jabatan[0] }}</span>
                        </div>
                        <div class="mb-3">
                            <label>Jenis Kelamin</label>
                            <select v-model="kelolapengguna.jeniskelamin" class="form-control">
                                <option value="" disabled>Pilih Jenis Kelamin</option>
                                <option v-for="option in jenisKelaminOptions" :key="option.value" :value="option.value">
                                    {{ option.label }}
                                </option>
                            </select>
                            <span class="text-danger" v-if="this.errorList.jeniskelamin">{{ this.errorList.jeniskelamin[0]
                            }}</span>
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
                            <button type="submit" class="btn btn-primary">Simpan</button>
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
    name: "kelolapenggunaCreate",
    data() {
        return {
            kelolapengguna: {
                nama: '',
                email: '',
                jabatan: '',
                jeniskelamin: '',
                telp: '',
                koderfid: '',
                faceid: '',
                fingerprint: '',
            },
            isLoading: false,
            isLoadingTitle: 'Loading',
            errorList: {},
            jabatanOptions: [
                { value: 'Managers', label: 'Managers' },
                { value: 'Staff', label: 'Staff' },
                { value: 'Oprasional', label: 'Oprasional' },
                { value: 'Operator', label: 'Operator' },
                { value: 'OB', label: 'OB' },
            ],
            jenisKelaminOptions: [
                { value: 'Laki-laki', label: 'Laki-laki' },
                { value: 'Perempuan', label: 'Perempuan' },
            ],

        };
    },
    methods: {
        savekelolapengguna() {
            this.isLoading = true;
            this.isLoadingTitle = "Saving";

            var myThis = this;

            axios.post('http://localhost:8000/api/kelolapengguna', this.kelolapengguna)
                .then(res => {
                    console.log(res, 'res');
                    alert(res.data.message);

                    // Membersihkan input setelah berhasil disimpan
                    this.kelolapengguna.nama = '';
                    this.kelolapengguna.email = '';
                    this.kelolapengguna.jabatan = '';
                    this.kelolapengguna.jeniskelamin = '';
                    this.kelolapengguna.telp = '';
                    this.kelolapengguna.koderfid = '';
                    this.kelolapengguna.faceid = '';
                    this.kelolapengguna.fingerprint = '';

                    this.isLoading = false;
                    this.isLoadingTitle = "Loading";

                    // Navigasi kembali ke halaman kelolaPengguna
                    this.$router.push('/kelolaPengguna');
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

<style></style>