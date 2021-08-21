<template>
  <div id="app" class="flex flex-col h-screen">
    <header>
      <h1 class="m-4 text-3xl font-bold text-indigo-500">Crypto Market</h1>
    </header>
    <main class="mb-auto">
      <div class="flex shadow-md mb-5 text-xs w-11/12 mt-4 m-auto">
        <span
          class="bg-indigo-500 w-28 font-bold text-center text-gray-200 p-3 px-5 rounded-l"
          >Search</span
        ><input
          class="field text-sm text-gray-600 p-2 px-3 rounded-r w-full"
          type="text"
          placeholder="Bitcoins, Ethereum, ..."
          v-model="crypto_search"
        />
      </div>
      <Table
        :titles="[
          '#',
          'Crypto',
          'Price',
          'Price change percentage 24h',
          'Total volume',
        ]"
        :cryptos="crypto_copi"
      />
    </main>

    <div class="border-t-2 bg-indigo-500 text-center py-4 mt-2 text-white">
      <p class="text-2xl">
        <span class="font-semibold">|</span> This website was developed by
        <a
          href="https://github.com/JoseAlmando/"
          class="text-red-300"
          target="_blank"
          rel="noreferrer"
        >
          José Almando Dominique
        </a>
        <span class="font-semibold">|</span>
      </p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Table from "./components/Table.vue";
export default {
  name: "App",
  components: {
    Table,
  },
  data() {
    return {
      cryptos: [],
      crypto_copi: [],
      crypto_search: "",
    };
  },
  mounted() {
    axios
      .get(
        "https://api.coingecko.com/api/v3/coins/markets?vs_currency=USD&order=market_cap_desc&per_page=100&page=1&sparkline=false"
      )
      .then((res) => {
        this.cryptos = res.data;
        this.crypto_copi = this.cryptos;
      });
  },
  watch: {
    crypto_search: function() {
      this.crypto_copi = this.cryptos.filter(
        (crypto) =>
          crypto.name
            .toLowerCase()
            .includes(this.crypto_search.toLowerCase()) ||
          crypto.symbol
            .toLowerCase()
            .includes(this.crypto_search.toLowerCase()) ||
          crypto.id.toLowerCase().includes(this.crypto_search.toLowerCase())
      );
    },
  },
};
</script>

<style>
body {
  font-family: "Montserrat", sans-serif;
  background: #f3f4f6;
}
</style>
