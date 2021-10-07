<template>
  <main v-if="!loading">
    <CountrySelect @get-country="getCountryData" :countries="countries"/>

    <button @click="clearCountryData"
            v-if="status.Country"
        class="bg-purple-700 text-white rounded p-2 mt-3
                    focus:outline-none hover:bg-purple-600">
      Clear Country
    </button>
    <br>
    <DataTitle :text="title" :dataDate="dataDate"/>
    <DataBoxes :status="status"/>
    
  </main>


  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="require('../assets/hourglass.gif')" alt="" class="w-24 m-auto" />
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle";
import DataBoxes from "@/components/DataBoxes";
import CountrySelect from "@/components/CountrySelect";

export default {
  name: 'Home',
  components: {
  DataTitle,
    DataBoxes,
    CountrySelect
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      status: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif')
    }
  },
  methods:{
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary')
      const data =await res.json()
      return data
    },
    getCountryData(country) {
      this.status = country
      this.title = country.Country
      this.dataDate = country.Date

    },
    async clearCountryData() {
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.status = data.Global
      this.loading = false
    }
  },
  async created() {
    const data = await this.fetchCovidData()
    console.log(data)

    this.dataDate = data.Date
    this.status = data.Global
    this.countries = data.Countries
    this.loading = false
  }
}
</script>
