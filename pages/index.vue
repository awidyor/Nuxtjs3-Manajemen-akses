<template>
  <div>
    <Header />
    <Footer />

    <!-- Informasi Total dalam Card Terpisah -->
    <div class="my-5" style="display: flex; justify-content: center; align-items: center; width: 50%; margin: 0 auto;">

      <!-- Card Total Masuk -->
      <!-- Kartu Total Masuk -->
      <div class="card shadow text-center" style="width: 30%; margin-right: 5%;">
        <div class="card-body d-flex flex-row align-items-center">
          <svg xmlns="http://www.w3.org/2000/svg" width="50" height="50" fill="currentColor"
            class="bi bi-box-arrow-in-right" viewBox="0 0 16 16">
            <path fill-rule="evenodd"
              d="M6 3.5a.5.5 0 0 1 .5-.5h8a.5.5 0 0 1 .5.5v9a.5.5 0 0 1-.5.5h-8a.5.5 0 0 1-.5-.5v-2a.5.5 0 0 0-1 0v2A1.5 1.5 0 0 0 6.5 14h8a1.5 1.5 0 0 0 1.5-1.5v-9A1.5 1.5 0 0 0 14.5 2h-8A1.5 1.5 0 0 0 5 3.5v2a.5.5 0 0 0 1 0z" />
            <path fill-rule="evenodd"
              d="M11.854 8.354a.5.5 0 0 0 0-.708l-3-3a.5.5 0 1 0-.708.708L10.293 7.5H1.5a.5.5 0 0 0 0 1h8.793l-2.147 2.146a.5.5 0 0 0 .708.708l3-3z" />
          </svg>
          <div>
            <h5 class="card-title mb-0">Total Masuk</h5>
            <h6 class="d-flex justify-content-end fs-2 mt-2">{{ totalMasuk }}</h6>
          </div>
        </div>
      </div>

      <!-- Kartu Total Keluar -->
      <div class="card shadow text-center" style="width: 30%; margin-right: 5%;">
        <div class="card-body d-flex flex-row align-items-center">
          <svg xmlns="http://www.w3.org/2000/svg" width="50" height="50" fill="currentColor" class="bi bi-box-arrow-right"
            viewBox="0 0 16 16">
            <path fill-rule="evenodd"
              d="M10 12.5a.5.5 0 0 1-.5.5h-8a.5.5 0 0 1-.5-.5v-9a.5.5 0 0 1 .5-.5h8a.5.5 0 0 1 .5.5v2a.5.5 0 0 0 1 0v-2A1.5 1.5 0 0 0 9.5 2h-8A1.5 1.5 0 0 0 0 3.5v9A1.5 1.5 0 0 0 1.5 14h8a1.5 1.5 0 0 0 1.5-1.5v-2a.5.5 0 0 0-1 0z" />
            <path fill-rule="evenodd"
              d="M15.854 8.354a.5.5 0 0 0 0-.708l-3-3a.5.5 0 0 0-.708.708L14.293 7.5H5.5a.5.5 0 0 0 0 1h8.793l-2.147 2.146a.5.5 0 0 0 .708.708l3-3z" />
          </svg>
          <div>
            <h5 class="card-title mb-0" style="margin-left: 5px;">Total Keluar</h5>
            <h6 class="d-flex justify-content-end fs-2 mt-2">{{ totalKeluar }}</h6>
          </div>
        </div>
      </div>



      <!-- Card Total Pengguna -->
      <div class="card shadow text-center" style="width: 35%;">
        <div class="card-body d-flex flex-row align-items-center">
          <svg xmlns="http://www.w3.org/2000/svg" width="50" height="50" fill="currentColor" class="bi bi-people-fill"
            viewBox="0 0 16 16">
            <path
              d="M7 14s-1 0-1-1 1-4 5-4 5 3 5 4-1 1-1 1zm4-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6m-5.784 6A2.238 2.238 0 0 1 5 13c0-1.355.68-2.75 1.936-3.72A6.325 6.325 0 0 0 5 9c-4 0-5 3-5 4s1 1 1 1zM4.5 8a2.5 2.5 0 1 0 0-5 2.5 2.5 0 0 0 0 5" />
          </svg>
          <div>
            <h5 class="card-title  mb-0 " style="margin-left: 5px;">Total Pengguna</h5>
          <h6 class="d-flex justify-content-end fs-2 mt-2">{{ totalPengguna }}</h6>
          </div>

        </div>
      </div>
    </div>

    <!-- Grafik -->
    <div class="d-flex justify-content-center mt-3">

      <!-- Kartu grafik Bulanan -->
      <div class="card shadow rounded text-center" style="width: 40%;">
        <div class="card-header">
          <h6>Bulanan</h6>
        </div>
        <div class="card-body p-0">
          <canvas ref="chartCanvasBulanan"></canvas>
        </div>
      </div>

      <!-- Kartu grafik Mingguan -->
      <div class="card shadow text-center" style="width: 40%; margin-left: 20px;">
        <div class="card-header">
          <h6>Mingguan</h6>
        </div>
        <div class="card-body p-0">
          <canvas ref="chartCanvasMingguan"></canvas>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { Chart, registerables } from 'chart.js';

export default {
  middleware: 'auth',
  
  name: 'SmallCenteredGrafikComponent',
  setup() {
    const chartCanvasBulanan = ref(null);
    const chartCanvasMingguan = ref(null);
    const totalMasuk = ref('100');
    const totalKeluar = ref('50');
    const totalPengguna = ref('200');

    onMounted(() => {
      Chart.register(...registerables);

      // Kode grafik untuk Bulanan
      const dataBulanan = {
        labels: ['Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun', 'Jul'],
        datasets: [
          { label: 'Fingerprint', data: [10, 15, 20, 25, 30, 35, 40], backgroundColor: 'rgba(255, 99, 132, 0.2)' },
          { label: 'Face ID', data: [5, 10, 15, 20, 25, 30, 35], backgroundColor: 'rgba(54, 162, 235, 0.2)' },
          { label: 'Tap Card', data: [15, 20, 25, 30, 35, 40, 45], backgroundColor: 'rgba(255, 206, 86, 0.2)' },
        ],
      };

      const ctxBulanan = chartCanvasBulanan.value.getContext('2d');
      if (ctxBulanan) {
        new Chart(ctxBulanan, {
          type: 'bar',
          data: dataBulanan,
          options: {
            layout: {
              padding: {
                top: 20,
                right: 30,
                bottom: 20,
                left: 30
              }
            }
          }
        });
      }

      // Kode grafik untuk Mingguan
      const dataMingguan = {
        labels: ['M1', 'M2', 'M3', 'M4'],
        datasets: [
          { label: 'Fingerprint', data: [5, 7, 10, 8], backgroundColor: 'rgba(255, 99, 132, 0.2)' },
          { label: 'Face ID', data: [2, 4, 6, 5], backgroundColor: 'rgba(54, 162, 235, 0.2)' },
          { label: 'Tap Card', data: [7, 9, 12, 10], backgroundColor: 'rgba(255, 206, 86, 0.2)' },
        ],
      };

      const ctxMingguan = chartCanvasMingguan.value.getContext('2d');
      if (ctxMingguan) {
        new Chart(ctxMingguan, {
          type: 'bar',
          data: dataMingguan,
          options: {
            layout: {
              padding: {
                top: 20,
                right: 30,
                bottom: 20,
                left: 30
              }
            }
          }
        });
      }
    });

    // Mengembalikan semua variabel dan referensi yang diperlukan
    return {
      chartCanvasBulanan,
      chartCanvasMingguan,
      totalMasuk,
      totalKeluar,
      totalPengguna
    };
  },
}


</script>

<style scoped>
/* Gaya CSS Anda di sini, jika diperlukan */
</style>
