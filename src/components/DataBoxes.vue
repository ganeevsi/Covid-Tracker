<template>
  <div class="grid md:grid-cols-3 gap-4">
    <!-- Box 1 -->
    <div class="shadow-md bg-blue-500 p-10 text-center rounded">
      <h3 class="text-3xl text-black-900 font-bold mb-4">Cases</h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{ numberWithCommas(status.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithCommas(status.TotalConfirmed) }}
      </div>
    </div>

    <!-- Box 2 -->
    <div class="shadow-md bg-red-500 p-10 text-center rounded">
      <h3 class="text-3xl text-black-900 font-bold mb-4">Deaths</h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{ numberWithCommas(status.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithCommas(status.TotalDeaths) }}
      </div>
    </div>

    <!-- Box 3 -->
    <div class="shadow-md bg-green-500 p-10 text-center rounded">
      <h3 class="text-3xl text-black-900 font-bold mb-4">Recovered</h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{ numberWithCommas(status.NewRecovered) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithCommas(status.TotalRecovered) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ['status'],
  methods: {
    numberWithCommas (x) {
      return x.toString()
          .replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    }
  }
}
</script>

<style scoped>

</style>