<template>
  <div id="viewDeck">
    <div id="viewLrigDeckLayout">
      <span>ルリグデッキ</span>
      <ul id="viewLrigDeck">
        <li v-for="card in lrigCards" :key="card">
          <div class="cardLayout">
            <div class="imageLayout">
              <img :src="card.img" class="cardImage">
              <img :src="card.img" class="cardImage" v-if="card.count >= 2">
              <img :src="card.img" class="cardImage" v-if="card.count >= 3">
              <img :src="card.img" class="cardImage" v-if="card.count >= 4">
            </div>
            <div class="countLayout">
              <div class="count">{{ card.count }}枚</div>
            </div>
          </div>
        </li>
      </ul>
    </div>
    <div id="viewMainDeckLayout" :style="{ '--viewMainDeckWidthCount': adjustMainDeckWidth() }">
      <span>メインデッキ</span>
      <ul id="viewMainDeck">
        <li v-for="card in mainCards" :key="card">
          <div class="cardLayout">
            <div class="imageLayout">
              <img :src="card.img" class="cardImage">
              <img :src="card.img" class="cardImage" v-if="card.count >= 2">
              <img :src="card.img" class="cardImage" v-if="card.count >= 3">
              <img :src="card.img" class="cardImage" v-if="card.count >= 4">
            </div>
            <div class="countLayout">
              <div class="count">{{ card.count }}枚</div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
    name: 'ViewMode',
    props: {
      lrigCards: Array,
      mainCards: Array,
    },
    methods: {
      adjustMainDeckWidth() {
        return Math.max((this.mainCards.length + 2) / 3, 4);
      }
    }
}
</script>
<style>
:root {
    --viewImageWidth: 160px;
    --viewImageHeight: calc(var(--viewImageWidth) / 5 * 7);
    --viewImageShift: calc(var(--viewImageWidth) / 40);
    --viewImageCountFontSize: calc(var(--viewImageWidth) / 8);
    --viewLrigDeckWidth: calc((var(--viewImageWidth) + var(--viewImageShift) * 7) * 4);
    --viewMainDeckWidthCount: 4;
}

ul {
    padding-inline-start: 0px;
}

.cardImage {
    width: 120px;
    height: auto;
}

#viewLrigDeck,
#viewMainDeck {
    text-align: left;
    padding-left: calc(var(--viewImageShift) * 7);
}

#viewLrigDeck li,
#viewMainDeck li {
    display: inline-block;
}

#viewDeck #viewLrigDeckLayout,
#viewDeck #viewMainDeckLayout {
    display: inline-block;
    position: relative;
    vertical-align: top;
}

#viewDeck #viewLrigDeckLayout {
    width: var(--viewLrigDeckWidth);
}

#viewDeck #viewMainDeckLayout {
    width: calc((var(--viewImageWidth) + var(--viewImageShift) * 7) * var(--viewMainDeckWidthCount));
}

#viewDeck .cardLayout {
    margin-bottom: calc(var(--viewImageShift) * 4);
}

#viewDeck .cardLayout .imageLayout {
    width: var(--viewImageWidth);
    height: var(--viewImageHeight);
    margin-right: calc(var(--viewImageShift) * 5);
    margin-bottom: calc(var(--viewImageShift) * 4);
    position: relative;
}

#viewDeck .cardLayout .countLayout div.count {
    width: var(--viewImageWidth);
    font-size: var(--viewImageCountFontSize);
    text-align: center;
}

#viewDeck .cardLayout .imageLayout .cardImage {
    width: var(--viewImageWidth);
    height: auto;
    position: absolute;
    border-radius: 7px;
}

#viewDeck .cardLayout .imageLayout .cardImage:nth-child(1) {
    left: 0;
    top: 0;
    z-index: 4;
}

#viewDeck .cardLayout .imageLayout .cardImage:nth-child(2) {
    left: calc(var(--viewImageShift) * 1);
    top: calc(var(--viewImageShift) * 1);
    z-index: 3;
}

#viewDeck .cardLayout .imageLayout .cardImage:nth-child(3) {
    left: calc(var(--viewImageShift) * 2);
    top: calc(var(--viewImageShift) * 2);
    z-index: 2;
}

#viewDeck .cardLayout .imageLayout .cardImage:nth-child(4) {
    left: calc(var(--viewImageShift) * 3);
    top: calc(var(--viewImageShift) * 3);
    z-index: 1;
}
</style>