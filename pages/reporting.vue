<template>
       <Header /> 
     <Footer /> 
     
     
  <div>
    <div class="card mt-5 me-4 ms-4 me-4">
      <!-- Card Body untuk Tampilan Biasa -->
      <div class="card-body">
        <div class="mb-3">
          <button @click="exportToPDF" class="btn btn-primary me-2">Export to PDF</button>
          <button @click="exportToExcel" class="btn btn-success me-2">Export to Excel</button>
          <button @click="printReport" class="btn btn-info ">Print Report</button>
        </div>
        <div class="card-body print-body" id="printTable">
          <table class="table">
            <!-- Tabel -->
            <thead>
              <tr class="text-center">
                <th>No.</th>
                <th>Nama</th>
                <th>Jabatan</th>
                <th>Jenis Kelamin</th>
                <th>Tempat Masuk</th>
                <th>Metode Masuk</th>
                <th>Metode Keluar</th>
                <th>Waktu Masuk</th>
                <th>Waktu Keluar</th>
              </tr>
            </thead>
            <tbody>
              <tr class="text-center" v-for="(item, index) in reporting" :key="item.id">
                <td>{{ index + 1 }}</td>
                <td>{{ item.nama }}</td>
                <td>{{ item.jabatan }}</td>
                <td>{{ item.jeniskelamin }}</td>
                <td>{{ item.tempatmasuk }}</td>
                <td>{{ item.metodemasuk }}</td>
                <td>{{ item.metodekeluar }}</td>
                <td>{{ item.waktumasuk }}</td>
                <td>{{ item.waktukeluar }}</td>
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
  data() {
    return {
      reporting: [],
    };
  },
  mounted() {
    this.fetchReportingData();
  },
  methods: {
    async fetchReportingData() {
      try {
        const response = await axios.get('http://localhost:3001/reporting');
        this.reporting = response.data;
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    exportToPDF() {
      // Implementasi logika ekspor PDF
    },
    exportToExcel() {
      // Implementasi logika ekspor Excel
    },
    printReport() {
      this.printTable('printTable');
    },
    printTable(tableId) {
      let printContents = document.getElementById(tableId).innerHTML;
      let originalContents = document.body.innerHTML;

      document.body.innerHTML = printContents;

      window.print();

      document.body.innerHTML = originalContents;
    },
  },
};
</script>

<style scoped>
  @media print {
    .card-body:not(.print-body) {
      visibility: hidden;
    }

    .print-body {
      font-size: 5px; /* Sesuaikan dengan ukuran font yang diinginkan */
    }
  }
</style>

