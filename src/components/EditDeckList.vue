<template>
    <ul>
        <li v-for="(card, index) in cards" :key="card" draggable="true"
        @dragstart="onDragStart(index)" @dragover.prevent
        @dragend="onDragEnd()" @drop="onDrop(index)">
            <div class="cardLayout">
                <img :src="card.img" class="cardImage">
                <div class="countLayout">
                    <div class="changeCount" @click="minusCard(card, cards, index)">－</div>
                    <div class="count">{{ card.count }}</div>
                    <div class="changeCount" @click="plusCard(card)">＋</div>
                </div>
                <div class="lifeburst" v-if="showLB">
                    <img src="../img/lifeburst.svg" width="20" :class="{ lb: card.lifeburst }"
                    @click="switchLB(card)">
                </div>
            </div>
        </li>
    </ul>
</template>
<script>
export default {
    name: 'EditDeckList',
    props: {
        cards: Array,
        showLB: Boolean,
    },
    data() {
        return {
            moving: undefined
        }
    },
    methods: {
        minusCard(card, cards, i) {
            if (card.count > 1) {
                card.count--;
            } else if (card.count === 1) {
                cards.splice(i, 1);
            }
        },
        plusCard(card) {
            if (card.count < 4) {
                card.count++;
            }
        },
        onDragStart(index) {
            this.moving = index;
        },
        onDragEnd() {
            this.moving = undefined;
        },
        onDrop(at) {
            const index = this.moving;
            const cards = this.cards;
            if (index === undefined || index === at
                || index > cards.length -1 || at > cards.length - 1) {
                return;
            }
            const value = cards[index];
            const tail = cards.slice(index + 1);
            cards.splice(index);
            Array.prototype.push.apply(cards, tail);
            cards.splice(at, 0, value);
            this.moving = undefined;
            return;
        },
        switchLB(card) {
            card.lifeburst = !card.lifeburst;
        }
    }
}
</script>
<style scoped>
.cardImage {
    user-drag: none;
    -webkit-user-drag: none;
    -moz-user-select: none;
    width: 120px;
    height: auto;
}

ul {
    width: 1200px;
    text-align: left;
    margin: auto;
    min-height: 200px;
}

li {
    display: inline-block;
}

.cardLayout .countLayout div {
    display: table-cell;
    text-align:center;
}

.cardLayout .countLayout div.changeCount {
    width: 20px;
    cursor: pointer;
}

.cardLayout .countLayout div.count {
    width: 80px;
}

.lifeburst {
    text-align: center;
}

.lifeburst img {
    cursor: pointer;
    opacity: 0.1;
}

.lifeburst img.lb {
    opacity: 1;
}
</style>