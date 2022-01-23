<template>

    <table cellspacing="5" :key="situation">
        <tbody>
            <tr 
                class="row"
                v-for="(card1, i1) in cards"
                :key="card1"
            >
                <td
                    :class="{
                        cell: true,
                        [getCardClass(handLabel(card1, card2, i1, i2))]: true
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
    <!-- <div
        id="key"
        style="margin: 5px">
        <span class="red">3bet</span>
        <span class="green">raise/fold</span>
        <span class="blue">call</span>
        <span class="grey">limp/raise</span>
        <span class="yellow">limp/call</span>
        <span class="pink">limp/fold</span>
        <span class="white">fold</span>
    </div> -->

</template>

<script>

export default {
    props: {
        situation: {
            type: String
        }
    },
    data() {
        return {
            cards: "AKQJT98765432".split(''),
            // RFI
            ljrfi: "AA AKs AQs AJs ATs A9s A8s A7s A6s A5s A4s A3s A2s AKo KK KQs KJs KTs K9s K8s AQo KQo QQ QJs QTs Q9s AJo KJo QJo JJ JTs J9s ATo TT T9s 99 88 77 66",
            hjrfi: "AA AKs AQs AJs ATs A9s A8s A7s A6s A5s A4s A3s A2s AKo KK KQs KJs KTs K9s K8s K7s K6s AQo KQo QQ QJs QTs Q9s Q8s AJo KJo QJo JJ JTs J9s ATo KTo QTo TT T9s 99 98s 88 87s 77 76s 66 55",
            corfi: "AA AKs AQs AJs ATs A9s A8s A7s A6s A5s A4s A3s A2s AKo KK KQs KJs KTs K9s K8s K7s K6s K5s K4s K3s AQo KQo QQ QJs QTs Q9s Q8s Q7s Q6s AJo KJo QJo JJ JTs J9s J8s ATo KTo QTo JTo TT T9s T8s T7s A9o 99 98s 97s A8o 88 87s 77 76s 66 55 44 33",
            btnrfi: "AA AKs AQs AJs ATs A9s A8s A7s A6s A5s A4s A3s A2s AKo KK KQs KJs KTs K9s K8s K7s K6s K5s K4s K3s K2s AQo KQo QQ QJs QTs Q9s Q8s Q7s Q6s Q5s Q4s Q3s AJo KJo QJo JJ JTs J9s J8s J7s J6s J5s J4s ATo KTo QTo JTo TT T9s T8s T7s T6s A9o K9o Q9o J9o T9o 99 98s 97s 96s A8o K8o T8o 98o 88 87s 86s 85s A7o 77 76s 75s A6o 66 65s 64s A5o 55 54s 53s A4o 44 33 22",
            sbrfi: {
                raiseOr4Bet: "AKs KK AQo QQ AJo KJo JJ",
                raiseAndCall: "ATs A9s A8s A7s A5s KJs KTs K8s K5s QJs QTs JTs T9s K9o Q9o J9o 98o 65s 54s 33 22",
                raiseAndFold: "K3s K2s Q5s Q4s Q3s Q2s J7s J6s J5s J4s T6s T5s 96s A8o K8o T8o A7o K7o A6o 64s 53s A4o",
                limpAndRaise: "AA AQs AJs AKo KQs K9s Q9s J9s TT 99 98s 88 87s",
                limpAndCall: "A6s A4s A3s A2s K7s K6s K4s KQo Q8s Q7s Q6s QJo J8s ATo KTo QTo JTo T8s T7s A9o T9o 97s 86s 85s 77 76s 75s 66 A5o 55 44",
                limpAndFold: "J3s J2s T4s T3s 95s 94s Q8o J8o 84s Q7o J7o T7o 97o 87o 74s K6o Q6o 86o 76o 63s K5o Q5o K4o 43s A3o A2o",
            },
            // LJ vs 3bet
            ljvshj3bet: {
                fourBetForValue: "AA AKs AKo KK QQ",
                fourBetAsABluff: "A9s A8s A5s A4s A3s A2s KQo AJo",
                call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JJ JTs TT T9s 99 98s 88 77",
                fold: "A7s A6s K9s Q9s KJo J9s ATo 87s 76s 66 65s 55 44"
            },
            ljvsco3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ",
                fourBetAsABluff: "A9s A8s A5s A4s A3s A2s KQo AJo",
                call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JTs TT T9s 99 98s 88 77 66",
                fold: "A7s A6s K9s Q9s KJo J9s ATo 87s 76s 65s 55 44"
            },
            ljvsbtn3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ",
                fourBetAsABluff: "A9s A8s A7s A5s A5s A4s A3s A2s KQo AJo 76s",
                call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JTs TT T9s 99 98s 88 87s 77 66 55",
                fold: "A6s K9s Q9s KJo J9s ATo 65s 44"
            },
            ljcssb3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ",
                fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s ATo KJo",
                call: "AQs AJs ATs KQs KJs KTs AQo KQo QJs QTs AJo JTs J9s TT T9s 99 98s 88 87s 77 76s 66 55",
                fold: "K9s Q9s 65s 44"
            },
            ljcsbb3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ",
                fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s AJo KQo",
                call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JTs TT T9s 99 98s 88 87s 77 76s 66 55 44",
                fold: "K9s Q9s KJo J9s ATo 65s"
            },
            // HJ vs RFI
            hjvsljrfi: "AA AKs AQs AJs ATs A5s AKo KK KQs KJs KTs AQo KQo QQ QJs JJ TT 99",
            // HJ vs 3BET
            hjvsco3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ",
                fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s KJo ATo 76s",
                call: "AQs AJs ATs KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s TT T9s 99 98s 88 87s 77 66 55",
                fold: "K8s QJo T8s 97s 65s 54s 44 33 22"
            },
            hjvsbtn3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ",
                fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s KJo ATo 76s 65s 54s",
                call: "AQs AJs ATs KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s TT T9s 99 98s 88 87s 77 66 55 44",
                fold: "K8s QJo T8s 97s 65s 54s 33 22"
            },
            hjvssb3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ",
                fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s KJo ATo",
                call: "AQs AJs ATs KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s TT T9s 99 98s 88 87s 77 76s 66 55 44",
                fold: "K8s QJo T8s 97s 65s 54s 33 22"
            },
            hjvsbb3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ",
                fourBetAsABluff: "A9s A8s A7s A6s A5s A4s A3s A2s KQo AJo",
                call: "AQs AJs ATs KQs KJs KTs AQo QJs QTs JTs TT T9s 99 98s 88 87s 77 76s 66 55 44",
                fold: "K9s K8s Q9s KJo QJo J9s ATo T8s 97s 65s 54s 33 22"
            },
            // CO vs RFI
            covsljrfi: "AA AKs AQs AJs ATs A5s AKo KK KQs KJs KTs AQo KQo QQ QJs JJ TT 99 88",
            covshjrfi: "AA AKs AQs AJs ATs A9s A5s A4s AKo KK KQs KJs KTs AQo KQo QQ QJs AJo JJ TT 99 88",
            // CO vs 3BET
            covsbtnsb3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ TT",
                fourBetAsABluff: " A8s A7s A6s A4s A3s A2s KJo ATo 97s 86s 75s 54s",
                call: "AQs AJs ATs A9s A5s KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s T9s T8s 99 98s 88 87s 77 76s 66 65s 55 44",
                fold: "K8s K7s Q8s QJo J8s KTo QTo JTo A9o 64s 43s 33 22"
            },
            covsbb3bet: {
                fourBetForValue: "AA AKs AKo KK QQ JJ TT",
                fourBetAsABluff: "A8s A4s A3s A2s KJo ATo T8s 97s 65s 54s",
                call: "AQs AJs ATs A9s A5s KQs KJs KTs K9s AQo KQo QJs QTs Q9s AJo JTs J9s T9s 99 98s 88 87s 77 76s 66 55 44",
                fold: "A7s A6s K8s K7s Q8s QJo J8s KTo QTo JTo A9o 86s 75s 64s 43s 33 22"
            },
            // BTN
            btnvsljrfi: {
                threeBet: "AA AKs AQs A9s A8s A4s A3s AKo KK K9s KQo QQ QJs AJo JJ T9s",
                call: "AJs ATs A5s KQs KJs KTs AQo QTs JTs TT 99 88 77 76s 66 65s 55 54s"
            },
            btnvshjrfi: {
                threeBet: "AA AKs AQs A9s A8s A7s A4s A3s AKo KK KTs K9s K8s KQo QQ QTs Q9s AJo JJ T9s 66",
                call: "AJs ATs A5s KQs KJs AQo QJs JTs TT 99 98s 88 87s 77 55 44"
            },
            btnvscorfi: {
                threeBet: "AA AKs AQs A8s A7s A6s A4s A3s AKo KK KQs K9s KQo QQ QJs Q9s AJo KJo QJo JJ JTs J9s ATo TT 55",
                call: "AJs ATs A9s A5s KJs KTs AQo QTs T9s 99 98s 88 77 66"
            },
            // BTN vs 3BET
            btnvssbbb3bet: {
                fourBetForValue: "AA AKs AQs AJs AKo KK AQo QQ JJ TT 99",
                fourBetAsABluff: "K6s K5s K4s Q7s J7s QTo JTo K9o A8o 86s 75s 64s A5o 54s A4o 43s A3o",
                call: "ATs A9s A8s A7s A6s A5s A4s A3s A2s KQs KJs KTs K9s K8s K7s KQo QJs QTs Q9s Q8s AJo KJo QJo JTs J9s J8s ATo KTo T9s T8s T7s A9o 98s 97s 88 87s 77 76s 66 65s 55 44 33 22",
                fold: "K3s K2s Q6s Q5s Q4s Q3s Q2s J6s T6s Q9o J9o T9o 96s K8o Q8o J8o T8o 98o 85s A7o K7o 97o 87o 74s A6o 76o 53s 32s A2o"
            },
            // SB
            sbvsljrfi: "AA AKs AQs AJs ATs A5s AKo KK KQs KJs KTs AQo QQ QJs JJ TT 99",
            sbvshjrfi: "AA AKs AQs AJs ATs A5s AKo KK KQs KJs KTs AQo QQ QJs QTs JJ JTs TT 99 88 77",
            sbvscorfi: "AA AKs AQs AJs ATs A9s A5s AKo KK KQs KJs KTs AQo KQo QQ QJs QTs AQo KQo QQ QJs QTs JJ JTs J9s TT T9s 99 88 77 66",
            sbvsbtnrfi: "AA AKs AQs AJs ATs A9s A8s A7s A5s A4s AKo KK KQs KJs KTs K9s AQo KQo QQ QJs QTs Q9s AJo KJ0 JJ JTs J9s TT T9s T8s 99 88 77 66 55",
            // SB RFI vs 3BET
            sbrfivsbb3bet: {
                fourBetForValue: "AA AKs AQs AJs AKo KK AQo QQ JJ",
                fourBetAsABluff: "J4s Q5o Q4o K3o K2o ",
                call: "ATs KQs KJs KQo QJs AJo KJo ATo TT 99 95s 88 85s 74s 43s",
                fold: "J3s J2s T5s T4s 94s 84s J6o T6o 96o 86o 63s 53s Q3o Q2o"
            },
            // SB Limp vs BB Raise
            sblimpvsbbraise: {
                fourBetForValue: "AA AKs AQs AJs ATs AKo KK KQs KJs AQo KQo QQ QJs AJo KJo JJ ATo TT 99 88",
                threeBetAsABluff: "Q7o K6o K5o A3o A2o",
                call: "A9s A8s A7s A6s A5s A4s A3s A2s KTs K9s K8s K7s K6s K5s K4s K3s K2s QTs Q9s Q9s Q8s Q7s Q6s Q5s Q4s Q3s Q2s QJo JTs J9s J8s J7s J6s J5s J4s J3s J2s KTo QTo JTo J9s J8s J7s J6s J5s KTo Qto JTo T9s T8s T7s T6s KTo QTo JTo T9s T8s T7s T6s KTo QTo JTo T9s T8s T7s T6s A9o K9o Q9o J9o T9o 98s 97s 96s A8o K8o Q8o J8o T8o 98o 87s 86s A7o K7o 97o 87o 77 76s 75s A6o 76o 66 65s 64s A5o 55 54s A4o 44 33 32s 22",
                fold: "J7o T7o Q6o 65o K4o"
            },
            // BB
            bbvsljrfi: {
                threeBet: "AA AKs AQs A5s A4s AKo KK KQs KJs QQ QJs JJ JTs 65s 54s",
                call: "AJs ATs A9s A8s A7s A6s A3s A2s KTs K9s K8s K7s K6s K5s K4s K3s K2s AQo KQo QTs Q9s Q8s Q7s Q6s Q5s AJo KJo QJo J9s J8s ATo JTo TT T9s T8s T7s 99 98s 97s 96s 88 87s 86s 85s 77 76s 75s 74s 66 64s 63s 55 53s 44 43s 33 32s 22" 
            },
            bbvshjrfi: {
                threeBet: "AA AKs AQs A9s A5s A4s AKo KK KQs KJs KTs K5s QQ QJs QTs JJ JTs TT 65s 54s",
                call: "AJs ATs A8s A7s A6s A3s A2s K9s K8s K7s K6s K4s K3s K2s AQo KQo Q9s Q8s Q7s Q6s Q5s AJo KJo QJo J9s J8s J7s ATo KTo QTo JTo T9s T8s T7s A9o 99 98s 97s 96s 88 87s 86s 85s 77 76s 75s 74s 66 64s 63s 55 53s 44 43s 33 22" 
            },
            bbvscorfi: {
                threeBet: "AA AKs AQs AJs A9s A5s A4s AKo KK KQs KJs KTs AQo QQ QJs QTs Q9s JJ JTs J9s TT T9s 99 65s 54s",
                call: "ATs A8s A7s A6s A3s A2s K9s K8s K7s K6s K5s K4s K3s K2s KQo Q8s Q7s Q6s Q5s Q4s Q3s AJo KJo QJo J8s J7s J6s ATo KTo QTo JTo T8s T7s A9o T9o 98s 97s 96s A8o 88 87s 86s 85s 77 76s 75s 74s 66 64s 63s A5o 55 53s 52s 44 43s 33 22" 
            },
            bbvsbtnrfi: {
                threeBet: "AA AKs AQs AJs ATs A6s A5s A4s AKo KKs KQs KJs KTs K9s AQo KQo QQ QJs QTs Q9s JJ JTs J9s J8s TT T9s T8s 99 98s 97s 88 87s 76s 65s 54s",
                call: "A9s A8s A7s A3s A2s K8s K7s K6s K5s K4s K3s K2s Q8s Q7s Q6s Q5s Q4s Q3s Q2s AJo KJo QJo J7s J6s J5s J4s J3s J2s ATo KTo QTo JTo T7s T6s T5s T4s T3s T2s A9o K9o Q9o J9o T9o 96s 95s 94s A8o K8o Q8o J8o T8o 98o 86s 85s 84s A7o K7o 87o 77 75s 74s 73s A6o K6o 76o 66 64s 63s 62s A5o 65o 55 53s 52s A4o 54o 44 43s 42s 33 32s 22"  
            },
            bbvssblimp: {
                threeBet: "AA AKs AQs AJs ATs A9s A8s A5s A4s A3s AKo KK KQs KJs KTs K9s K6s K5s AQo KQo QQ QJs QTs Q9s AJo KJo JJ JTs J9s J8s J2s ATo JTo TT T9s T8s T4s T3s T3s T2s T9o 99 98s 97s 94s 93s 92s 88 87s 86s 84s J7o 77 76s 75s 74s 73s Q6o J6o T6o 96o 66 65s 64s 63s A5o K5o Q5o J5o T5o 95o 85o 75o 55 54s K4o Q4o 74o 44 33 32s",
                call: "A7s A6s A2s K8s K7s K4s K3s K2s Q8s Q7s Q6s Q5s Q4s Q3s Q2s QJo J7s J6s J5s J4s J3s KTo QTo T7s T6s T5s A9o K9o Q9o J9o 96s 95s A8o K8o Q8o J8o T8o 98o 85s 83s 82s A7o K7o Q7o T7o 97o 87o 72s A6o K6o 86o 76o 62s 65o 53s 52s A4o J4o T4o 94o 84o 64o 54o 43s 42s A3o K3o Q3o J3o T3o 93o 83o 73o 63o 53o 43o A2o K2o Q2o J2o T2o 92o 82o 72o 62o 52o 42o 32o 22"  
            },
            bbvssbraise: {
                threeBet: "AA AKs AQs AJs ATs A5s A4s AKo KK KQs KJs KTs AQo QQ QJs JJ J5s TT T5s 99 95s J8o 88 87s J7o T7o 76s A6o K6o Q6o 65s K5o 54s",
                call: "A9s A8s A7s A6s A3s A2s K9s K8s K7s K6s K5s K4s K3s K2s KQo QTs Q9s Q8s Q7s Q6s Q5s Q4s Q3s Q2s AJo KJo QJo JTs J9s J8s J7s J6s J4s J3s J2s ATo KTo QTo JTo T9s T8s T7s T6s T4s T3s T2s A9o K9o Q9o J9o T9o 98s 97s 96s 96s 94s 93s 92s A8o K8o Q8o T8o 98o 86s 85s 84s A7o K7o Q7o 97o 87o 77 75s 74s 73s 86o 76o 66 64s 63s 62s A5o 65o 55 53s 52s A4o 54o 44 43s 42s A3o 33 32s A2o"  
            },
        
        
        }
    },
    methods: {
        handLabel(card1, card2, i1, i2) {
            const holeCards = i1 < i2 ? `${card1}${card2}` : `${card2}${card1}`
            const suited = i1 < i2 ? 's' : 'o' && card1 === card2 ? '' : 'o' 
            return `${holeCards}${suited}`
        },
        getCardClass(label) {
            // LJ RFI
            if (this.situation === "LJ RFI") {
                if (this.ljrfi.includes(label)) {
                    return 'red'
                }
            };
            // HJ RFI
            if (this.situation === "HJ RFI") {
                if (this.hjrfi.includes(label)) {
                    return 'red'
                }
            };
            // CO RFI
            if (this.situation === "CO RFI") {
                if (this.corfi.includes(label)) {
                    return 'red'
                }
            };
            // BTN RFI
            if (this.situation === "BTN RFI") {
                if (this.btnrfi.includes(label)) {
                    return 'red'
                }
            };
            // SB RFI
            if (this.situation === "SB RFI") {
                if (this.sbrfi.raiseOr4Bet.includes(label)) {
                    return 'red'
                };
                if (this.sbrfi.raiseAndCall.includes(label)) {
                    return 'blue'
                };
                if (this.sbrfi.raiseAndFold.includes(label)) {
                    return 'green'
                };
                if (this.sbrfi.limpAndRaise.includes(label)) {
                    return 'grey'
                };
                if (this.sbrfi.limpAndCall.includes(label)) {
                    return 'yellow'
                };
                if (this.sbrfi.limpAndFold.includes(label)) {
                    return 'pink'
                };
            };
            // LJ vs HJ 3bet
            if (this.situation === "LJ vs HJ 3bet") {
                if (this.ljvshj3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.ljvshj3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.ljvshj3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.ljvshj3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // LJ vs CO 3bet
            if (this.situation === "LJ vs CO 3bet") {
                if (this.ljvsco3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.ljvsco3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.ljvsco3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.ljvsco3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // LJ vs BTN 3bet
            if (this.situation === "LJ vs BTN 3bet") {
                if (this.ljvsbtn3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.ljvsbtn3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.ljvsbtn3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.ljvsbtn3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // LJ vs SB 3bet
            if (this.situation === "LJ vs SB 3bet") {
                if (this.ljcssb3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.ljcssb3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.ljcssb3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.ljcssb3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // LJ vs BB 3bet
            if (this.situation === "LJ vs BB 3bet") {
                if (this.ljcsbb3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.ljcsbb3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.ljcsbb3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.ljcsbb3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // HJ vs LJ RFI
            if (this.situation === "HJ vs LJ RFI") {
                if (this.hjvsljrfi.includes(label)) {
                    return 'red'
                }
            };
            // CO vs LJ RFI
            if (this.situation === "CO vs LJ RFI") {
                if (this.covsljrfi.includes(label)) {
                    return 'red'
                }
            };
            // CO vs HJ RFI
            if (this.situation === "CO vs HJ RFI") {
                if (this.covshjrfi.includes(label)) {
                    return 'red'
                }
            };
            // BTN vs LJ RFI
            if (this.situation === "BTN vs LJ RFI") {
                if (this.btnvsljrfi.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.btnvsljrfi.call.includes(label)) {
                    return 'blue'
                }
            };
            // BTN vs HJ RFI
            if (this.situation === "BTN vs HJ RFI") {
                if (this.btnvshjrfi.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.btnvshjrfi.call.includes(label)) {
                    return 'blue'
                }
            };
            // BTN vs CO RFI
            if (this.situation === "BTN vs CO RFI") {
                if (this.btnvscorfi.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.btnvscorfi.call.includes(label)) {
                    return 'blue'
                }
            };
            // SB vs LJ RFI
            if (this.situation === "SB vs LJ RFI") {
                if (this.sbvsljrfi.includes(label)) {
                    return 'red'
                }
            };
            // SB vs HJ RFI
            if (this.situation === "SB vs HJ RFI") {
                if (this.sbvshjrfi.includes(label)) {
                    return 'red'
                }
            };
            // SB vs CO RFI
            if (this.situation === "SB vs CO RFI") {
                if (this.sbvscorfi.includes(label)) {
                    return 'red'
                }
            };
            // SB vs BTN RFI
            if (this.situation === "SB vs BTN RFI") {
                if (this.sbvsbtnrfi.includes(label)) {
                    return 'red'
                }
            };
            // BB vs LJ RFI
            if (this.situation === "BB vs LJ RFI") {
                if (this.bbvsljrfi.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.bbvsljrfi.call.includes(label)) {
                    return 'blue'
                }
            };
            // BB vs HJ RFI
            if (this.situation === "BB vs HJ RFI") {
                if (this.bbvshjrfi.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.bbvshjrfi.call.includes(label)) {
                    return 'blue'
                }
            };
            // BB vs CO RFI
            if (this.situation === "BB vs CO RFI") {
                if (this.bbvscorfi.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.bbvscorfi.call.includes(label)) {
                    return 'blue'
                }
            };
            // BB vs BTN RFI
            if (this.situation === "BB vs BTN RFI") {
                if (this.bbvsbtnrfi.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.bbvsbtnrfi.call.includes(label)) {
                    return 'blue'
                }
            };
            // BB vs SB LIMP
            if (this.situation === "BB vs SB Limp") {
                if (this.bbvssblimp.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.bbvssblimp.call.includes(label)) {
                    return 'blue'
                }
            };
            // BB vs SB RAISE
            if (this.situation === "BB vs SB Raise") {
                if (this.bbvssbraise.threeBet.includes(label)) {
                    return 'red'
                }
                if (this.bbvssbraise.call.includes(label)) {
                    return 'blue'
                }
            };
            // HJ vs CO 3bet
            if (this.situation === "HJ vs CO 3bet") {
                if (this.hjvsco3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.hjvsco3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.hjvsco3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.hjvsco3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // HJ vs BTN 3bet
            if (this.situation === "HJ vs BTN 3bet") {
                if (this.hjvsbtn3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.hjvsbtn3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.hjvsbtn3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.hjvsbtn3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // HJ vs SB 3bet
            if (this.situation === "HJ vs SB 3bet") {
                if (this.hjvssb3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.hjvssb3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.hjvssb3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.hjvssb3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // HJ vs BB 3bet
            if (this.situation === "HJ vs BB 3bet") {
                if (this.hjvsbb3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.hjvsbb3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.hjvsbb3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.hjvsbb3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // CO vs BTN/SB 3bet
            if (this.situation === "CO vs BTN/SB 3bet") {
                if (this.covsbtnsb3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.covsbtnsb3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.covsbtnsb3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.covsbtnsb3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // CO vs BB 3bet
            if (this.situation === "CO vs BB 3bet") {
                if (this.covsbb3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.covsbb3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.covsbb3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.covsbb3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // BTN vs SB/BB 3bet
            if (this.situation === "BTN vs SB/BB 3bet") {
                if (this.btnvssbbb3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.btnvssbbb3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.btnvssbbb3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.btnvssbbb3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // SB RFI vs BB 3bet
            if (this.situation === "SB RFI vs BB 3bet") {
                if (this.sbrfivsbb3bet.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.sbrfivsbb3bet.fourBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.sbrfivsbb3bet.call.includes(label)) {
                    return 'green'
                };
                if (this.sbrfivsbb3bet.fold.includes(label)) {
                    return 'grey'
                };
            };
            // SB Limp vs BB Raise
            if (this.situation === "SB Limp vs BB Raise") {
                if (this.sblimpvsbbraise.fourBetForValue.includes(label)) {
                    return 'red'
                };
                if (this.sblimpvsbbraise.threeBetAsABluff.includes(label)) {
                    return 'blue'
                };
                if (this.sblimpvsbbraise.call.includes(label)) {
                    return 'green'
                };
                if (this.sblimpvsbbraise.fold.includes(label)) {
                    return 'grey'
                };
            };
        }
    },
    watch: {
        situation() {
            // console.log(this.situation)
         }
    }
}
</script>

<style scoped>

.cell {
    /* border: 1px solid black; */
    border-radius: 3px;
    height: 25px;
    width: 25px;
    font-size: 14px;
    text-align: center;
    background-color: white;
}

#key span {
    padding: 5px;
    margin: 2px;
}

.red {
    background-color: rgb(204, 16, 16);
    color: white;
}

.blue {
    background-color: rgb(12, 12, 167);
    color: white;
}
.grey {
    background-color: rgb(116, 116, 116);
    color: white;
}
.yellow {
    background-color: rgb(226, 226, 12);
}
.pink {
    background-color: pink;
}
.green {
    background-color: rgb(10, 114, 10);
    color: white;
}
.white {
    background-color: white;
}
</style>