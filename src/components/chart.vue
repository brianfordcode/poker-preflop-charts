<template>
    <table cellspacing="2">
        <tbody>
            <tr
                class="row"
                v-for="(card1, i1) in cards"
                :key="card1"
            >
                <td 
                    class="cell"
                    v-for="(card2, i2) in cards"
                    :key="card2"
                >
                {{ handLabel(card1, card2, i1, i2) }}
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>

export default {
    data() {
        return {
            cards: "AKQJT98765432".split('') //["A", "K", "Q", "J", "T", "9", "8", "7", "6", "5", "4", "3", "2"]
        }
    },
    methods: {
        handLabel(card1, card2, i1, i2) {
            const holeCards = i1 < i2 ? `${card1}${card2}` : `${card2}${card1}`
            const suited = i1 < i2 ? 's' : 'o' && card1 === card2 ? '' : 'o'
            return `${holeCards}${suited}`
        }
    }
    // computed: {
    //     makeChart() {
    //         cards.forEach((card1, i1) => {
    //             let row = ''
    //             cards.forEach((card2, i2) => {
    //                 row += `${card1} - ${card2} ${i1 < i2 ? 'a' : 'b'},`
    //             })
    //         return row
    //         })
    //     }
    // }
}
</script>

<style scoped>

.cell {
    border: 1px solid black;
    border-radius: 3px;
    height: 25px;
    width: 25px;
    font-size: 14px;
    text-align: center;
}

</style>