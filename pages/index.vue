<template>
  <!-- <Tutorial/> -->
  <div>
    <div class="text-center mt-4">
      <button type="button" class="btn btn-primary btn-sm" @click="refresh()">Refresh</button>
    </div>
    <table class="table mt-2">
      <tbody :style="{ 'background-color': '#fffdd0', 'color': '#000' }">
        <tr :style="{ 'background-color': '#fffdd0', 'color': '#000' }" v-for="bitcoin in btc">
          <th scope="row" class="text-center">
            Rank <br>
            {{ btc.rank }}
          </th>
          <td class="text-center">
            {{ btc.name }} <br>
            {{ btc.symbol }}
          </td>
          <td class="text-center"> 
            USD <br>
            {{ btc.price_usd }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  //wkwk
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      bitcoin: [],
      items: [
        { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
        { age: 21, first_name: 'Larsen', last_name: 'Shaw' },
        { age: 89, first_name: 'Geneva', last_name: 'Wilson' },
        { age: 38, first_name: 'Jami', last_name: 'Carney' }
      ]
    }
  },

  mounted() {
    this.getData();
  },

  methods: {
    async getData() {
      const response = await fetch(`https://api.coinlore.net/api/tickers`, {
        method: 'GET',
        headers: {
          accept: 'application/json'
        },
      });

      if (!response.ok) {
        console.log('Error');
      }

      const result = await response.json();
      this.bitcoin = result;
      return result;
    },

    async refresh() {
      await this.getData();
    },
  }
}
</script>
