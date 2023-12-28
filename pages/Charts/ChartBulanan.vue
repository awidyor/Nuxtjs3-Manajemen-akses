<template>
    <div class="container mt-5">
      <div class="card">
        <div class="card-header">
          Histogram Bulanan
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
      labels: [
        'January', 'February', 'March', 'April', 'May', 'June',
        'July', 'August', 'September', 'October', 'November', 'December'
      ],
      datasets: [
        {
          label: 'Face ID',
          data: [150, 120, 100, 80, 90, 110, 130, 140, 160, 170, 180, 200], // Ganti dengan data sebenarnya
          backgroundColor: 'rgba(255, 99, 132, 0.2)',
          borderColor: 'rgba(255, 99, 132, 1)',
          borderWidth: 1,
        },
        {
          label: 'Fingerprint',
          data: [80, 90, 110, 130, 140, 160, 170, 180, 200, 150, 120, 100], // Ganti dengan data sebenarnya
          backgroundColor: 'rgba(54, 162, 235, 0.2)',
          borderColor: 'rgba(54, 162, 235, 1)',
          borderWidth: 1,
        },
        {
          label: 'Tap Card',
          data: [100, 120, 150, 130, 110, 90, 80, 70, 60, 50, 40, 30], // Ganti dengan data sebenarnya
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
  