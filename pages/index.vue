<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline"> โปรแกรมคิดเงินทอน </v-card-title>
        <v-card-text>
          <v-text-field
            v-model="productPrice"
            label="ราคาสินค้า"
            type="number"
          ></v-text-field>
          <v-text-field
            v-model="money"
            label="รับเงิน"
            type="number"
          ></v-text-field>

          <div>ทอน {{ changeCoin }} บาท</div>
          <div>500 : {{ bankAndCoin.bank500.length }} ใบ</div>
          <div>100 : {{ bankAndCoin.bank100.length }} ใบ</div>
          <div>50 : {{ bankAndCoin.bank50.length }} ใบ</div>
          <div>10 : {{ bankAndCoin.coin10.length }} เหรียญ</div>
          <div>5 : {{ bankAndCoin.coin5.length }} เหรียญ</div>
          <div>1 : {{ bankAndCoin.coin1.length }} เหรียญ</div>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      ans: [],
      money: 0,
      productPrice: 0,
      bankAndCoin: {
        bank500: [],
        bank100: [],
        bank50: [],
        coin10: [],
        coin5: [],
        coin1: [],
      },
    };
  },
  watch: {
    changeCoin(val) {
      this.changeCoin = val;
    },
  },
  computed: {
    changeCoin() {
      let bankAndCoin = [500, 100, 50, 10, 5, 1];
      let money = this.money;
      let productPrice = this.productPrice;
      let change = 0;
      change = money - productPrice;
      let size = bankAndCoin.length;
      this.findMinCoins(bankAndCoin, size, change);
      if (change > 0) {
        return change;
      } else {
        return 0;
      }
    },
  },
  methods: {
    findMinCoins(bankAndCoin, size, change) {
      let i = 0;
      let count = 0;

      for (i = 0; i < size; i++) {
        while (change >= bankAndCoin[i]) {
          change -= bankAndCoin[i];
          this.ans[count] = bankAndCoin[i];
          count++;
        }
        if (change == 0) break;
      }
      this.ans.forEach((element) => {
        if (element == 500) {
          this.bankAndCoin.bank500.push(element);
        }
        if (element == 100) {
          this.bankAndCoin.bank100.push(element);
        }
        if (element == 50) {
          this.bankAndCoin.bank50.push(element);
        }
        if (element == 10) {
          this.bankAndCoin.coin10.push(element);
        }
        if (element == 5) {
          this.bankAndCoin.coin5.push(element);
        }
        if (element == 1) {
          this.bankAndCoin.coin1.push(element);
        }
      });
    },
  },
};
</script>
