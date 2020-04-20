<template>
  <div class="mesure">
    <div class="form-group d-flex justify-content-center mt-3">
      <label class="col-5 col-sm-2 col-form-label">調味料</label>
      <select v-model="input" @change="seasoningSelect" class="col-sm-3">
        <option
          v-for="seasoning in seasonings"
          :value="seasoning.name"
          :key="seasoning.name"
        >{{ seasoning.name }}</option>
      </select>
    </div>
    <div v-if="input != ''" class="mt-5">
      <div class="form-group d-flex justify-content-center">
        <label class="col-5 col-sm-2 col-form-label">大さじ</label>
        <input
          type="number"
          v-model="amount.tbsp"
          @change="tbspChange"
          class="col-sm-3"
          pattern="\d*"
        />
      </div>
      <div class="form-group d-flex justify-content-center">
        <label class="col-5 col-sm-2 col-form-label">小さじ</label>
        <input
          type="number"
          v-model="amount.tsp"
          @change="tspChange"
          class="col-sm-3"
          pattern="\d*"
        />
      </div>
      <div class="form-group d-flex justify-content-center">
        <label class="col-5 col-sm-2 col-form-label">グラム</label>
        <input
          type="number"
          v-model="amount.gram"
          @change="gramChange"
          class="col-sm-3"
          pattern="\d*"
        />
      </div>
      <p>
        <small>※分量はおよそです。</small>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: "",
      amount: { tbsp: 1, tsp: 3, gram: 0 },
      target: { name: "", coefficient: 0 },
      seasonings: [
        { name: "ウスターソース", coefficient: 6 },
        { name: "オリーブオイル", coefficient: 6 },
        { name: "片栗粉", coefficient: 3 },
        { name: "カレー粉", coefficient: 2 },
        { name: "牛乳", coefficient: 5 },
        { name: "グラニュー糖", coefficient: 4 },
        { name: "ケチャップ", coefficient: 5 },
        { name: "ココアパウダー", coefficient: 2 },
        { name: "こしょう", coefficient: 2 },
        { name: "粉チーズ", coefficient: 2 },
        { name: "コーヒー", coefficient: 2 },
        { name: "ごま", coefficient: 3 },
        { name: "小麦粉", coefficient: 3 },
        { name: "酒", coefficient: 5 },
        { name: "サラダ油", coefficient: 4 },
        { name: "ざらめ", coefficient: 5 },
        { name: "塩", coefficient: 6 },
        { name: "ショートニング", coefficient: 4 },
        { name: "上白糖", coefficient: 3 },
        { name: "しょうゆ", coefficient: 6 },
        { name: "酢", coefficient: 5 },
        { name: "バター", coefficient: 4 },
        { name: "はちみつ", coefficient: 7 },
        { name: "ベーキングパウダー", coefficient: 4 },
        { name: "マヨネーズ", coefficient: 4 },
        { name: "味噌", coefficient: 6 },
        { name: "みりん", coefficient: 6 },
        { name: "ラード", coefficient: 4 }
      ]
    };
  },
  methods: {
    seasoningSelect() {
      if (this.input == "") {
        this.amount = { tbsp: 1, tsp: 3, gram: 0 };
        return;
      }
      let input = this.input;
      this.target = this.seasonings.filter(function(item, index) {
        if (item.name.indexOf(input) >= 0) return true;
      });
      this.amount.gram = this.target[0].coefficient * 3 * this.amount.tsp;
    },
    tbspChange() {
      this.amount.tsp = this.amount.tbsp * 3;
      this.amount.gram = this.target[0].coefficient * 3 * this.amount.tsp;
    },
    tspChange() {
      this.amount.tbsp = this.amount.tsp / 3;
      this.amount.gram = this.target[0].coefficient * 3 * this.amount.tsp;
    },
    gramChange() {
      this.amount.tsp = this.amount.gram / this.target[0].coefficient;
      this.amount.tbsp = this.amount.tsp / 3;
    }
  }
};
</script>

<style scoped>
input[type="number"] {
  text-align: right;
}
</style>
