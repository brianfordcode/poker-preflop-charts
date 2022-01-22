<template>

    <table cellspacing="2" cellpadding="0">
        <tbody>
            <!-- first row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in firstRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- second row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in secondRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- third row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in thirdRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- fourth row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in fourthRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- fifth row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in fifthRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- sixth row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in sixthRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- seventh row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in seventhRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- eighth row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in eighthRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- ninth row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in ninthRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- tenth row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in tenthRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- eleventh row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in eleventhRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- twelfth row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in twelfthRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
            <!-- thirteenth row -->
            <tr class="row">
                <td 
                    class="cell"
                    v-for="cards in thirteenthRow"
                    :key="cards"
                >
                {{ cards }}
                </td>
            </tr>
        </tbody>
    </table>

</template>

<script>
export default {
    data() {
        return {
            firstRow: ["AA","AKs","AQs","AJs","ATs","A9s","A8s","A7s","A6s","A5s","A4s","A3s","A2s"],
            secondRow: ["AKo","KK","KQs","KJs","KTs","K9s","K8s","K7s","K6s","K5s","K4s","K3s","K2s"],
            thirdRow: ["AQo","KQo","QQ","QJs","QTs","Q9s","Q8s","Q7s","Q6s","Q5s","Q4s","Q3s","Q2s"],
            fourthRow: ["AJo","KJo","QJo","JJ","JTs","J9s","J8s","J7s","J6s","J5s","J4s","J3s","J2s"],
            fifthRow: ["ATo","KTo","QTo","JTo","TT","T9s","T8s","T7s","T6s","T5s","T4s","T3s","T2s"],
            sixthRow: ["A9o","K9o","Q9o","J9o","T9o","99","98s","97s","96s","95s","94s","93s","92s"],
            seventhRow: ["A8o","K8o","Q8o","J8o","T8o","98o","88","87s","86s","85s","84s","83s","82s"],
            eighthRow: ["A7o","K7o","Q7o","J7o","T7o","97o","87o","77","76s","75s","74s","73s","72s"],
            ninthRow: ["A6o","K6s","Q6o","J6o","T6o","96o","86o","76o","66","65s","64s","63s","62s"],
            tenthRow: ["A5o","K5s","Q5o","J5o","T5o","95o","85o","75o","65o","55","54s","53s","52s"],
            eleventhRow: ["A4o","K4o","Q4o","J4o","T4o","94o","84o","74os","64o","54o","44","43s","42s"],
            twelfthRow: ["A3o","K3o","Q3o","J3o","T3o","93o","83o","73o","63o","53o","43o","33","32o"],
            thirteenthRow: ["A2o","K2o","Q2o","J2o","T2o","92o","82o","72o","62o","52o","42o","32o","22"],
        }
    }

}
</script>

<style scoped>

.cell {
    border: 1px solid black;
    border-radius: 3px;
    font-size: 14px;
    height: 30px;
    width: 30px;
    text-align: center;
}

</style>

