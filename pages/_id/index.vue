<template>
  <div>
    <h3 v-if="show == 1">Kelas 1(50-59)</h3>
    <h3 v-else-if="show == 2">Kelas 2(60-69)</h3>
    <h3 v-else-if="show == 3">Kelas 3(70-79)</h3>
    <h3 v-else-if="show == 4">Kelas 4(80-89)</h3>
    <h3 v-else-if="show == 5">Kelas 5(90-99)</h3>
    <h3 v-else-if="show == 6">Kelas 6(Memiliki C dan O pada nama)</h3>
    <TableData v-if="show == 1" :data="kelas1" :header="header" />
    <TableData v-else-if="show == 2" :data="kelas2" :header="header" />
    <TableData v-else-if="show == 3" :data="kelas3" :header="header" />
    <TableData v-else-if="show == 4" :data="kelas4" :header="header" />
    <TableData v-else-if="show == 5" :data="kelas5" :header="header" />
    <TableData v-else-if="show == 6" :data="kelas6" :header="header" />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data: () => ({
    allScore: [],
    kelas1: [],
    kelas2: [],
    kelas3: [],
    kelas4: [],
    kelas5: [],
    kelas6: [],
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
  computed: {
    show() {
      return this.$route.params.id
    },
  },
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
              this.kelas6.push(this.allScore[i])
            } else if (
              this.allScore[i].nilai <= 99 &&
              this.allScore[i].nilai >= 90
            ) {
              this.kelas5.push(this.allScore[i])
            } else if (
              this.allScore[i].nilai <= 89 &&
              this.allScore[i].nilai >= 80
            ) {
              this.kelas4.push(this.allScore[i])
            } else if (
              this.allScore[i].nilai <= 79 &&
              this.allScore[i].nilai >= 70
            ) {
              this.kelas3.push(this.allScore[i])
            } else if (
              this.allScore[i].nilai <= 69 &&
              this.allScore[i].nilai >= 60
            ) {
              this.kelas2.push(this.allScore[i])
            } else if (
              this.allScore[i].nilai <= 59 &&
              this.allScore[i].nilai >= 50
            ) {
              this.kelas1.push(this.allScore[i])
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
