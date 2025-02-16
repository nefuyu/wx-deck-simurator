<template>
  <div id="dragDropArea">
    <p class="dragDropInfo">画像をドラッグ＆ドロップでデッキに追加</p>
    <InputCard :cards="lrigCards" class="lrig"/>
    <InputCard :cards="mainCards" class="main"/>
  </div>
  <div id="deckArea">
    <span>ルリグデッキ</span> <span>{{ countLrigCards() }}枚</span>
    <EditDeckList :cards="lrigCards" :showLB="false"/>
    <span>メインデッキ</span> <span>{{ countMainCards() }}枚</span>&nbsp;
    <span>ライフバーストあり {{ countLB() }}枚</span> <span>ライフバーストなし {{ countNotLB() }}枚</span>
    <EditDeckList :cards="mainCards" :showLB="true"/>
  </div>
</template>

<script>
import InputCard from './InputCard.vue'
import EditDeckList from './EditDeckList.vue'

export default {
    name: 'EditMode',
    components: {
      InputCard,
      EditDeckList,
    },
    props: {
      lrigCards: Array,
      mainCards: Array,
    },
    methods: {
      countLrigCards() {
        return this.lrigCards.length === 0
          ? 0
          : this.lrigCards.reduce((i, j) => {return {"count": i.count + j.count};}).count;
      },
      countMainCards() {
        return this.mainCards.length === 0
          ? 0
          : this.mainCards.reduce((i, j) => {return {"count": i.count + j.count};}).count;
      },
      countLB() {
        const cards = this.mainCards.filter((card) => card.lifeburst === true);
        return cards.length === 0
          ? 0
          : cards.reduce((i, j) => {return {"count": i.count + j.count};}).count;
      },
      countNotLB() {
        const cards = this.mainCards.filter((card) => card.lifeburst === false);
        return cards.length === 0
          ? 0
          : cards.reduce((i, j) => {return {"count": i.count + j.count};}).count;
      }
    }
}
</script>