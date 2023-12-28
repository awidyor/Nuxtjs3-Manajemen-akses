<template>
  <div class=" container p-3 pb-3 mb-2 mt-4 px-1 rounded">
    <div class="card p-3">
      <div class="row p-3 text-center justify-content-center align-items-center">

        <div class="col-md-3 mb-3 ">
          <div class="card small-card ">
            <div class="card-body">
              <h5 class="card-title">Total Masuk</h5>
              <p class="card-text display-1 fw-semibold ">100</p>
            </div>
          </div>
        </div>

        <div class="col-md-3 mb-3">
          <div class="card small-card">
            <div class="card-body">
              <h5 class="card-title">Total Keluar</h5>
              <p class="card-text display-1 fw-semibold">90</p>
            </div>
          </div>
        </div>

        <div class="mt-5 px-1">
          <div class="card mb-5">
            <div class="card-header text-start">
              <h4>
                Grafik Histogram
                <button type="button" class="btn btn-outline-secondary btn-sm rounded-pill float-end"
                  style="font-size: 5px; padding: 0 5px;">
                  <NuxtLink to="/Charts/ChartBulanan" class="nav-link active">
                    Bulan
                  </NuxtLink>
                </button>

                <button type="button" class="btn btn-outline-secondary btn-sm rounded-pill float-end me-2"
                  style="font-size: 10px; padding: 0 5px;">
                  <NuxtLink to="/Charts/ChartMingguan" class="nav-link active">
                    Minggu
                  </NuxtLink>
                </button>
              </h4>
            </div>

            <div class="card-body p-5 overflow-x-auto overflow-y-hidden mb-5">
              <div class="row justify-content-center">
                <canvas ref="chartCanvas"></canvas>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script setup>
import { onMounted, ref } from 'vue';
import Chart from 'chart.js/auto';

const chartCanvas = ref(null);

onMounted(() => {
  const ctx = chartCanvas.value.getContext('2d');

  // Contoh data grafik (ganti dengan data sebenarnya)
  const data = {
    labels: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'],
    datasets: [
      {
        label: 'Face ID',
        data: [30, 40, 50, 60, 70, 80, 90], // Ganti dengan data sebenarnya
        backgroundColor: 'rgba(255, 99, 132, 0.2)',
        borderColor: 'rgba(255, 99, 132, 1)',
        borderWidth: 1,
      },
      {
        label: 'Fingerprint',
        data: [10, 20, 30, 40, 50, 60, 70], // Ganti dengan data sebenarnya
        backgroundColor: 'rgba(54, 162, 235, 0.2)',
        borderColor: 'rgba(54, 162, 235, 1)',
        borderWidth: 1,
      },
      {
        label: 'Tap Card',
        data: [5, 15, 25, 35, 45, 55, 65], // Ganti dengan data sebenarnya
        backgroundColor: 'rgba(255, 206, 86, 0.2)',
        borderColor: 'rgba(255, 206, 86, 1)',
        borderWidth: 1,
      },
    ],
  };

  // Konfigurasi grafik
  const options = {
    scales: {
      y: {
        beginAtZero: true,
      },
    },
  };

  // Inisialisasi grafik
  new Chart(ctx, {
    type: 'bar',
    data: data,
    options: options,
  });
});
</script>

  
<style scoped>
/* Style komponen jika diperlukan */
</style>