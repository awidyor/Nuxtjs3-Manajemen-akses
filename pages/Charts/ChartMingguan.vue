<template>
    <div class="container mt-5">
      <div class="card">
        <div class="card-header">
          Histogram Mingguan
        </div>
        <div class="card-body">
          <div class="row justify-content-center">
            <div class="col-8">
              <canvas ref="chartCanvas"></canvas>
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
  