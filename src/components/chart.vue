<template>

    <table cellspacing="5" :key="situation" class="chart">
        <tbody>
            <tr 
                class="row"
                v-for="(card1, i1) in cards"
                :key="card1"
            >
                <td
                    :class="{
                        hand: true,
                        [handLabel(card1, card2, i1, i2)]: true,
                        [getCardClass(handLabel(card1, card2, i1, i2))]: true,
                    }"
                    v-for="(card2, i2) in cards"
                    :key="card2"
                >
                {{ handLabel(card1, card2, i1, i2) }}
                </td>
            </tr>
        </tbody>
    </table>

    <!-- KEY -->
    <div class="key">
        <!-- All keys -->
        <div
            v-for="action in actions"
            :key="action"
            :class="[
                    getColor(action, this.situation),
                    showKeyItem(action, this.situation)
                    ]"
        >
        {{action}}
        </div>
        <!-- FOLD key -->
        <div
            v-if="situation != 'BB vs SB Limp'"
            style="background-color: white"
        >
        {{situation ? 'Fold' : 'Key'}}
        </div>
    </div>

</template>

<script>
import { registerRuntimeCompiler } from '@vue/runtime-core'

export default {
    props: {
        situation: {
            type: String
        }
    },
    data() {
        return {
            cards: "AKQJT98765432".split(''),
            actions: ['Raise', '3Bet','Call', 'Raise/4Bet', 'Raise/Call', 'Raise/Fold', 'Limp/Raise', 'Limp/Call', 'Limp/Fold', '4Bet for Value', '4Bet as Bluff', '3Bet as Bluff', '3Bet for Value'],
            recommendations: {
                // RFI
                "LJ RFI": {
                    raise: "AA AKs AQs AJs ATs A9s A8s A7s A6s A5s A4s A3s A2s AKo KK KQs KJs KTs K9s K8s AQo KQo QQ QJs QTs Q9s AJo KJo QJo JJ JTs J9s ATo TT T9s 99 88 77 66",
                },
                "HJ RFI": {
                    raise: "AA AKs AQs AJs ATs A9s A8s A7s A6s A5s A4s A3s A2s AKo KK KQs KJs KTs K9s K8s K7s K6s AQo KQo QQ QJs QTs Q9s Q8s AJo KJo QJo JJ JTs J9s ATo KTo QTo TT T9s 99 98s 88 87s 77 76s 66 55"
                },

                "CO RFI": {
                    raise: "AA AKs AQs AJs ATs A9s A8s A7s A6s A5s A4s A3s A2s AKo KK KQs KJs KTs K9s K8s K7s K6s K5s K4s K3s AQo KQo QQ QJs QTs Q9s Q8s Q7s Q6s AJo KJo QJo JJ JTs J9s J8s ATo KTo QTo JTo TT T9s T8s T7s A9o 99 98s 97s A8o 88 87s 77 76s 66 55 44 33",
                },
                "BTN RFI": {
                    raise: "AA AKs AQs AJs ATs A9s A8s A7s A6s A5s A4s A3s A2s AKo KK KQs KJs KTs K9s K8s K7s K6s K5s K4s K3s K2s AQo KQo QQ QJs QTs Q9s Q8s Q7s Q6s Q5s Q4s Q3s AJo KJo QJo JJ JTs J9s J8s J7s J6s J5s J4s ATo KTo QTo JTo TT T9s T8s T7s T6s A9o K9o Q9o J9o T9o 99 98s 97s 96s A8o K8o T8o 98o 88 87s 86s 85s A7o 77 76s 75s A6o 66 65s 64s A5o 55 54s 53s A4o 44 33 22",
                },
                "SB RFI": {
                    raiseOr4Bet: "AKs KK AQo QQ AJo KJo JJ",
                    raiseAndCall: "ATs A9s A8s A7s A5s KJs KTs K8s K5s QJs QTs JTs T9s K9o Q9o J9o 98o 65s 54s 33 22",
                    raiseAndFold: "K3s K2s Q5s Q4s Q3s Q2s J7s J6s J5s J4s T6s T5s 96s A8o K8o T8o A7o K7o A6o 64s 53s A4o",
                    limpAndRaise: "AA AQs AJs AKo KQs K9s Q9s J9s TT 99 98s 88 87s",
                    limpAndCall: "A6s A4s A3s A2s K7s K6s K4s KQo Q8s Q7s Q6s QJo J8s ATo KTo QTo JTo T8s T7s A9o T9o 97s 86s 85s 77 76s 75s 66 A5o 55 44",
                    limpAndFold: "J3s J2s T4s T3s 95s 94s Q8o J8o 84s Q7o J7o T7o 97o 87o 74s K6o Q6o 86o 76o 63s K5o Q5o K4o 43s A3o A2o",
                },
                // LJ vs 3bet
                "LJ vs HJ 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ",
                    fourBetAsABluff: "A9s A8s A5s A4s A3s A2s KQo AJo",
                    call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JJ JTs TT T9s 99 98s 88 77",
                },
                "LJ vs CO 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ",
                    fourBetAsABluff: "A9s A8s A5s A4s A3s A2s KQo AJo",
                    call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JTs TT T9s 99 98s 88 77 66",
                },
                "LJ vs BTN 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ",
                    fourBetAsABluff: "A9s A8s A7s A5s A5s A4s A3s A2s KQo AJo 76s",
                    call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JTs TT T9s 99 98s 88 87s 77 66 55",
                },
                "LJ vs SB 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ",
                    fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s ATo KJo",
                    call: "AQs AJs ATs KQs KJs KTs AQo KQo QJs QTs AJo JTs J9s TT T9s 99 98s 88 87s 77 76s 66 55",
                },
                "LJ vs BB 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ",
                    fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s AJo KQo",
                    call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JTs TT T9s 99 98s 88 87s 77 76s 66 55 44",
                },
                // HJ vs RFI
                "HJ vs LJ RFI": {
                    raise: "AA AKs AQs AJs ATs A5s AKo KK KQs KJs KTs AQo KQo QQ QJs JJ TT 99"
                },
                // HJ vs 3BET
                "HJ vs CO 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ",
                    fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s KJo ATo 76s",
                    call: "AQs AJs ATs KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s TT T9s 99 98s 88 87s 77 66 55",
                    fold: "K8s QJo T8s 97s 65s 54s 44 33 22"
                },
                "HJ vs BTN 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ",
                    fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s KJo ATo 76s 65s 54s",
                    call: "AQs AJs ATs KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s TT T9s 99 98s 88 87s 77 66 55 44",
                },
                "HJ vs SB 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ",
                    fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s KJo ATo",
                    call: "AQs AJs ATs KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s TT T9s 99 98s 88 87s 77 76s 66 55 44",
                },
                "HJ vs BB 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ",
                    fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s KQo AJo",
                    call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JTs TT T9s 99 98s 88 87s 77 76s 66 55 44",
                },
                // CO vs RFI
                "CO vs LJ RFI": {
                    raise: "AA AKs AQs AJs ATs A5s AKo KK KQs KJs KTs AQo KQo QQ QJs JJ TT 99 88"
                },
                "CO vs HJ RFI": {
                    raise: "AA AKs AQs AJs ATs A9s A5s A4s AKo KK KQs KJs KTs AQo KQo QQ QJs AJo JJ TT 99 88",
                },
                // CO vs 3BET
                "CO vs BTN/SB 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ TT",
                    fourBetAsABluff: " A8s A7s A6s A4s A3s A2s KJo ATo 97s 86s 75s 54s",
                    call: "AQs AJs ATs A9s A5s KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s T9s T8s 99 98s 88 87s 77 76s 66 65s 55 44",
                },
                "CO vs BB 3bet": {
                    fourBetForValue: "AA AKs AKo KK QQ JJ TT",
                    fourBetAsABluff: "A8s A4s A3s A2s KJo ATo T8s 97s 65s 54s",
                    call: "AQs AJs ATs A9s A5s KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s T9s 99 98s 88 87s 77 76s 66 55 44",
                },
                // BTN
                "BTN vs LJ RFI": {
                    threeBet: "AA AKs AQs A9s A8s A4s A3s AKo KK K9s KQo QQ QJs AJo JJ T9s",
                    call: "AJs ATs A5s KQs KJs KTs AQo QTs JTs TT 99 88 77 76s 66 65s 55 54s"
                },
                "BTN vs HJ RFI": {
                    threeBet: "AA AKs AQs A9s A8s A7s A4s A3s AKo KK KTs K9s K8s KQo QQ QTs Q9s AJo JJ T9s 66",
                    call: "AJs ATs A5s KQs KJs AQo QJs JTs TT 99 98s 88 87s 77 55 44"
                },
                "BTN vs CO RFI": {
                    threeBet: "AA AKs AQs A8s A7s A6s A4s A3s AKo KK KQs K9s KQo QQ QJs Q9s AJo KJo QJo JJ JTs J9s ATo TT 55",
                    call: "AJs ATs A9s A5s KJs KTs AQo QTs T9s 99 98s 88 77 66"
                },
                // BTN vs 3BET
                "BTN vs SB/BB 3bet": {
                    fourBetForValue: "AA AKs AQs AJs AKo KK AQo QQ JJ TT 99",
                    fourBetAsABluff: "K6s K5s K4s Q7s J7s QTo JTo K9o A8o 86s 75s 64s A5o 54s A4o 43s A3o",
                    call: "ATs A9s A8s A7s A6s A5s A4s A3s A2s KQs KJs KTs K9s K8s K7s KQo QJs QTs Q9s Q8s AJo KJo QJo JTs J9s J8s ATo KTo T9s T8s T7s A9o 98s 97s 88 87s 77 76s 66 65s 55 44 33 22",
                },
                // SB
                "SB vs LJ RFI": {
                    raise: "AA AKs AQs AJs ATs A5s AKo KK KQs KJs KTs AQo QQ QJs JJ TT 99"
                },
                "SB vs HJ RFI": {
                    raise: "AA AKs AQs AJs ATs A5s AKo KK KQs KJs KTs AQo QQ QJs QTs JJ JTs TT 99 88 77"
                },
                "SB vs CO RFI": {
                    raise: "AA AKs AQs AJs ATs A9s A5s AKo KK KQs KJs KTs AQo KQo QQ QJs QTs AQo KQo QQ QJs QTs JJ JTs J9s TT T9s 99 88 77 66"
                },
                "SB vs BTN RFI": {
                    raise: "AA AKs AQs AJs ATs A9s A8s A7s A5s A4s AKo KK KQs KJs KTs K9s AQo KQo QQ QJs QTs Q9s AJo KJ0 JJ JTs J9s TT T9s T8s 99 88 77 66 55"
                },
                // SB RFI vs 3BET
                "SB RFI vs BB 3bet": {
                    fourBetForValue: "AA AKs AQs AJs AKo KK AQo QQ JJ",
                    fourBetAsABluff: "J4s Q5o Q4o K3o K2o ",
                    call: "ATs KQs KJs KQo QJs AJo KJo ATo TT 99 95s 88 85s 74s 43s",
                },
                // SB Limp vs BB Raise
                "SB Limp vs BB Raise": {
                    fourBetForValue: "AA AKs AQs AJs ATs AKo KK KQs KJs AQo KQo QQ QJs AJo KJo JJ ATo TT 99 88",
                    threeBetAsABluff: "Q7o K6o K5o A3o A2o",
                    call: "A9s A8s A7s A6s A5s A4s A3s A2s KTs K9s K8s K7s K6s K5s K4s K3s K2s QTs Q9s Q9s Q8s Q7s Q6s Q5s Q4s Q3s Q2s QJo JTs J9s J8s J7s J6s J5s J4s J3s J2s KTo QTo JTo J9s J8s J7s J6s J5s KTo Qto JTo T9s T8s T7s T6s KTo QTo JTo T9s T8s T7s T6s KTo QTo JTo T9s T8s T7s T6s A9o K9o Q9o J9o T9o 98s 97s 96s A8o K8o Q8o J8o T8o 98o 87s 86s A7o K7o 97o 87o 77 76s 75s A6o 76o 66 65s 64s A5o 55 54s A4o 44 33 32s 22",
                },
                // BB
                "BB vs LJ RFI": {
                    threeBet: "AA AKs AQs A5s A4s AKo KK KQs KJs QQ QJs JJ JTs 65s 54s",
                    call: "AJs ATs A9s A8s A7s A6s A3s A2s KTs K9s K8s K7s K6s K5s K4s K3s K2s AQo KQo QTs Q9s Q8s Q7s Q6s Q5s AJo KJo QJo J9s J8s ATo JTo TT T9s T8s T7s 99 98s 97s 96s 88 87s 86s 85s 77 76s 75s 74s 66 64s 63s 55 53s 44 43s 33 32s 22" 
                },
                "BB vs HJ RFI": {
                    threeBet: "AA AKs AQs A9s A5s A4s AKo KK KQs KJs KTs K5s QQ QJs QTs JJ JTs TT 65s 54s",
                    call: "AJs ATs A8s A7s A6s A3s A2s K9s K8s K7s K6s K4s K3s K2s AQo KQo Q9s Q8s Q7s Q6s Q5s AJo KJo QJo J9s J8s J7s ATo KTo QTo JTo T9s T8s T7s A9o 99 98s 97s 96s 88 87s 86s 85s 77 76s 75s 74s 66 64s 63s 55 53s 44 43s 33 22" 
                },
                "BB vs CO RFI": {
                    threeBet: "AA AKs AQs AJs A9s A5s A4s AKo KK KQs KJs KTs AQo QQ QJs QTs Q9s JJ JTs J9s TT T9s 99 65s 54s",
                    call: "ATs A8s A7s A6s A3s A2s K9s K8s K7s K6s K5s K4s K3s K2s KQo Q8s Q7s Q6s Q5s Q4s Q3s AJo KJo QJo J8s J7s J6s ATo KTo QTo JTo T8s T7s A9o T9o 98s 97s 96s A8o 88 87s 86s 85s 77 76s 75s 74s 66 64s 63s A5o 55 53s 52s 44 43s 33 22" 
                },
                "BB vs BTN RFI": {
                    threeBet: "AA AKs AQs AJs ATs A6s A5s A4s AKo KKs KQs KJs KTs K9s AQo KQo QQ QJs QTs Q9s JJ JTs J9s J8s TT T9s T8s 99 98s 97s 88 87s 76s 65s 54s",
                    call: "A9s A8s A7s A3s A2s K8s K7s K6s K5s K4s K3s K2s Q8s Q7s Q6s Q5s Q4s Q3s Q2s AJo KJo QJo J7s J6s J5s J4s J3s J2s ATo KTo QTo JTo T7s T6s T5s T4s T3s T2s A9o K9o Q9o J9o T9o 96s 95s 94s A8o K8o Q8o J8o T8o 98o 86s 85s 84s A7o K7o 87o 77 75s 74s 73s A6o K6o 76o 66 64s 63s 62s A5o 65o 55 53s 52s A4o 54o 44 43s 42s 33 32s 22"  
                },
                "BB vs SB Limp": {
                    threeBet: "AA AKs AQs AJs ATs A9s A8s A5s A4s A3s AKo KK KQs KJs KTs K9s K6s K5s AQo KQo QQ QJs QTs Q9s AJo KJo JJ JTs J9s J8s J2s ATo JTo TT T9s T8s T4s T3s T3s T2s T9o 99 98s 97s 94s 93s 92s 88 87s 86s 84s J7o 77 76s 75s 74s 73s Q6o J6o T6o 96o 66 65s 64s 63s A5o K5o Q5o J5o T5o 95o 85o 75o 55 54s K4o Q4o 74o 44 33 32s",
                    call: "A7s A6s A2s K8s K7s K4s K3s K2s Q8s Q7s Q6s Q5s Q4s Q3s Q2s QJo J7s J6s J5s J4s J3s KTo QTo T7s T6s T5s A9o K9o Q9o J9o 96s 95s A8o K8o Q8o J8o T8o 98o 85s 83s 82s A7o K7o Q7o T7o 97o 87o 72s A6o K6o 86o 76o 62s 65o 53s 52s A4o J4o T4o 94o 84o 64o 54o 43s 42s A3o K3o Q3o J3o T3o 93o 83o 73o 63o 53o 43o A2o K2o Q2o J2o T2o 92o 82o 72o 62o 52o 42o 32o 22"  
                },
                "BB vs SB Raise": {
                    threeBet: "AA AKs AQs AJs ATs A5s A4s AKo KK KQs KJs KTs AQo QQ QJs JJ J5s TT T5s 99 95s J8o 88 87s J7o T7o 76s A6o K6o Q6o 65s K5o 54s",
                    call: "A9s A8s A7s A6s A3s A2s K9s K8s K7s K6s K5s K4s K3s K2s KQo QTs Q9s Q8s Q7s Q6s Q5s Q4s Q3s Q2s AJo KJo QJo JTs J9s J8s J7s J6s J4s J3s J2s ATo KTo QTo JTo T9s T8s T7s T6s T4s T3s T2s A9o K9o Q9o J9o T9o 98s 97s 96s 96s 94s 93s 92s A8o K8o Q8o T8o 98o 86s 85s 84s A7o K7o Q7o 97o 87o 77 75s 74s 73s 86o 76o 66 64s 63s 62s A5o 65o 55 53s 52s A4o 54o 44 43s 42s A3o 33 32s A2o"  
                },
            },
        }
    },
    methods: {
        handLabel(card1, card2, i1, i2) {
            const holeCards = i1 < i2 ? `${card1}${card2}` : `${card2}${card1}`
            const suited = i1 < i2 ? 's' : 'o' && card1 === card2 ? '' : 'o' 
            return `${holeCards}${suited}`
        },
        getCardClass(handLabel) {
            const recs = this.recommendations[this.situation]
            if (!recs) return ''
            const recommendationNames = Object.keys(recs)
            const classes = []
            recommendationNames.forEach(recommendationName => {
                if (recs[recommendationName].includes(handLabel)) {
                    classes.push(recommendationName)
                }
            })
            return classes.join(' ')
        },
        getColor(action, situation) {
            const colors = {
                "Raise": 'red',
                "3Bet": 'red',
                "Raise/4Bet": 'red',
                "4Bet for Value": 'red',
                "Raise/Call": 'blue',
                "4Bet as Bluff": 'blue',
                "3Bet as Bluff": 'blue',
                "Call": 'green',
                "Raise/Fold": 'green',
                "Limp/Raise": 'grey',
                "Limp/Call": 'yellow',
                "Limp/Fold": 'pink',
                "3Bet for Value": 'red'
            }
            if (typeof colors[action] === 'string') {
                return colors[action]
            }
            else if (colors[action]) {
                return colors[action][situation]
            }
        },
        showKeyItem(action, situation) {
            // if no situation chosen
            if (!situation) {return 'donotshow'}
            // RFI
            if (
                [
                "LJ RFI",
                "HJ RFI",
                "CO RFI",
                "BTN RFI"
                ].includes(situation)) {
                    if (action != 'Raise') {return 'donotshow'}
                }
            // SB RFI
            if (situation === "SB RFI") {
                if (action != 'Raise/4Bet' &&
                    action != 'Raise/Call' &&
                    action != 'Raise/Fold' &&
                    action != 'Limp/Raise' &&
                    action != 'Limp/Call' &&
                    action != 'Limp/Fold') {return 'donotshow'}
            }
            // SB Limp vs BB Raise
            if (situation === "SB Limp vs BB Raise") {
                if (action != "3Bet as Bluff" &&
                    action != "Call" &&
                    action != "3Bet for Value" &&
                    action != "Fold") {
                    return 'donotshow'
                }
            }
            // HJ, CO, SB VS RFI
            if ([
            "HJ vs LJ RFI",
            "CO vs LJ RFI",
            "CO vs HJ RFI",
            "SB vs LJ RFI",
            "SB vs HJ RFI",
            "SB vs CO RFI",
            "SB vs BTN RFI"
            ].includes(situation)) {
                if (action !='3Bet') {return 'donotshow'}
            }
            // BTN, BB VS RFI
            if ([
            "BTN vs LJ RFI",
            "BTN vs HJ RFI",
            "BTN vs CO RFI",
            "BB vs LJ RFI",
            "BB vs HJ RFI",
            "BB vs CO RFI",
            "BB vs BTN RFI",
            "BB vs SB Limp",
            "BB vs SB Raise"
            ].includes(situation)) {
                if (action !='3Bet' && action != 'Call') {return 'donotshow'}
            }
            // 3BET
            if ([
                "LJ vs HJ 3bet",
                "LJ vs CO 3bet",
                "LJ vs BTN 3bet",
                "LJ vs SB 3bet",
                "LJ vs BB 3bet",
                "HJ vs CO 3bet",
                "HJ vs BTN 3bet",
                "HJ vs SB 3bet",
                "HJ vs BB 3bet",
                "CO vs BTN/SB 3bet",
                "CO vs BB 3bet",
                "BTN vs SB/BB 3bet",
                "SB RFI vs BB 3bet"
                ].includes(situation)) {
                    if (action != '4Bet for Value' &&
                        action != '4Bet as Bluff' &&
                        action != 'Call' &&
                        action != 'Fold') {
                            return 'donotshow'
                    }
            }
        }
    },
}
</script>

<style scoped>

.chart {
    /* border: 1px solid; */
    /* height: auto; */
    /* position: relative; */
}

.hand {
    border-radius: 3px;
    height: 25px;
    width: 25px;
    font-size: 12px;
    text-align: center;
    background-color: white;
}

.key {
    display: flex;
    font-size: 11px;
    margin: 2px 0 5px 0;
}

.key div {
    padding: 5px;
}

.donotshow {
    display: none;
}

/* RED */
.red,
.raise,
.raiseOr4Bet,
.fourBetForValue,
.threeBet {
    background-color: rgb(204, 16, 16);
    color: white;
}

/* BLUE */
.blue,
.raiseAndCall,
.fourBetAsABluff,
.threeBetAsABluff {
    background-color: rgb(12, 12, 167);
    color: white;
}
/* GREY */
.grey,
.limpAndRaise {
    background-color: rgb(116, 116, 116);
    color: white;
}
/* YELLOW */
.yellow,
.limpAndCall {
    background-color: rgb(226, 226, 12);
}
/* PINK */
.pink,
.limpAndFold {
    background-color: pink;
}
/* GREEN */
.green,
.raiseAndFold,
.call {
    background-color: rgb(10, 114, 10);
    color: white;
}
</style>