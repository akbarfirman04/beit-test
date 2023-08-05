<template>
  <span>tes</span>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data: () => ({
    kelas1: [],
    kelas2: [],
    kelas3: [],
    kelas4: [],
    kelas5: [],
    kelas6: [],
  }),
  created() {
    this.getData()
  },
  methods: {
    async getData() {
      await axios({
        method: 'get',
        url: 'http://ecocim-backend-theone.beit.co.id/api/ManualConfig/TestBEIT',
      }).then(function (response) {
        console.log(response.data)
      })
    },
  },
}
</script>
