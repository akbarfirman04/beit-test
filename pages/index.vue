<template>
  <div>
    <h3>Semua Data</h3>
    <TableData :data="allScore" :header="header" />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data: () => ({
    allScore: [],
    months: [
      'Januari',
      'Februari',
      'Maret',
      'April',
      'Mei',
      'Juni',
      'Juli',
      'Agustus',
      'September',
      'Oktober',
      'November',
      'Desember',
    ],
    header: [
      { text: 'Nama', value: 'nama' },
      { text: 'Nilai', value: 'nilai' },
      { text: 'Tanggal Menikah', value: 'menikah' },
      { text: 'Tanggal Mati', value: 'mati' },
    ],
  }),
  created() {
    this.getData()
  },
  methods: {
    async getData() {
      await axios
        .get(
          'http://ecocim-backend-theone.beit.co.id/api/ManualConfig/TestBEIT'
        )
        .then((response) => {
          for (let i = 0; i < response.data.listNama.length; i++) {
            this.allScore.push({
              nama: response.data.listNama[i],
              nilai: response.data.listNilai[i],
              menikah: '-',
              mati: '-',
            })
          }
          for (let i = 0; i < this.allScore.length; i++) {
            if (this.isPrime(this.allScore[i].nilai)) {
              if (this.allScore[i].nilai % 10 < new Date().getMonth() + 1) {
                this.allScore[i].mati = `${
                  this.months[(this.allScore[i].nilai % 10) - 1]
                } ${new Date().getFullYear() + 1}`
              } else {
                this.allScore[i].mati = `${
                  this.months[(this.allScore[i].nilai % 10) - 1]
                } ${new Date().getFullYear()}`
              }
            }
            if (
              this.allScore[i].nama.includes('C') &&
              this.allScore[i].nama.includes('O')
            ) {
              if (this.allScore[i].nilai % 7 === 0) {
                this.allScore[i].menikah = '2024'
              }
            }
          }
        })
    },
    isPrime(num) {
      const sqrtnum = Math.floor(Math.sqrt(num))
      let prime = num !== 1
      for (let i = 2; i < sqrtnum + 1; i++) {
        // sqrtnum+1
        if (num % i === 0) {
          prime = false
          break
        }
      }
      return prime
    },
  },
}
</script>
