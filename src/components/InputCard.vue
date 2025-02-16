<template>
    <div class="DragDropArea"
        @dragover.prevent
        @drop="addCard">
        <input type="file" accept="image/*" name="photo">
    </div>
</template>
<script>
export default {
    name: 'EditDeckList',
    props: {
        cards: Array,
    },
    methods: {
        addCard(e) {
            const cards = this.cards;
            e.preventDefault();
            if (!e.dataTransfer?.files) return
            const reader = new FileReader();
            reader.onload = function() {
                const card = {
                    "img": reader.result,
                    "count": 1,
                    "lifeburst": false,
                };
                cards.push(card);
            };
            reader.readAsDataURL(e.dataTransfer.files[0]);
        }
    }
}
</script>
<style scoped>
.DragDropArea {
    display: inline-block;
    width: 150px;
    height: 210px;
    background-size: contain;
    background-repeat: no-repeat;
}

.lrig {
    background-image: url(../img/lrig.webp);
}

.main {
    background-image: url(../img/main.webp);
}

input {
    display: none;
}
</style>