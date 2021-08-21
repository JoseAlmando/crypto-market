<template>
  <div>
    <table
      class="w-11/12 table-auto m-auto text-center text-lg text-gray-400"
    >
      <thead>
        <tr class="bg-indigo-500 text-white">
          <th class="p-3" v-for="(title, index) in titles" :key="index">
            {{ title }}
          </th>
        </tr>
      </thead>
      <tbody class="bg-gray-200">
        <tr class="bg-white border-4 border-gray-100" v-for="(crypto, index) in cryptos" :key="index">
          <td class="py-2">{{ index + 1 }}</td>
          <td class="flex items-center py-2">
            <img
              :src="crypto.image"
              :alt="crypto.name"
              class="h-8 object-cover pr-3"
            />
            <span class="pr-3"> {{ crypto.name }} </span>
            <span class="text-gray-300">
              {{ crypto.symbol.toUpperCase() }}
            </span>
          </td>
          <td class="py-2">
            {{
              crypto.current_price.toLocaleString("en-US", {
                style: "currency",
                currency: "USD",
              })
            }}
          </td>
          <td class="py-2"
            :class="
              crypto.price_change_percentage_24h > 0
                ? 'text-green-500'
                : 'text-red-500'
            "
          >
            {{
              parseFloat(crypto.price_change_percentage_24h).toFixed(2) + "%"
            }}
          </td>
          <td class="py-2">  
            {{
              crypto.total_volume.toLocaleString("en-US", {
                style: "currency",
                currency: "USD",
              })
            }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Table",
  props: {
    titles: Array,
    cryptos: Array,
  },
};
</script>
