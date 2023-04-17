<template>
    <div class="w-full">
        <div class="flex flex-row mt-2" v-if="!winner">
            <button @click="roll()" class="bg-blue-500 w-1/5 ml-2 py-4 text-white text-2xl rounded-md" >
                Roll
            </button>

            <button class="bg-red-300 ml-2 text-black text-md rounded-full cursor-default" v-if="rolled_letter"
                style="height: 60px; width: 60px;"
            >
                {{ rolled_letter }}
            </button>

            <button class="bg-yellow-300 ml-2 text-black text-md rounded-full cursor-default" v-if="rolled_letter"
                style="height: 60px; width: 60px;"
            >
                {{ rolled_number }}
            </button>
        </div>

        <div class="mt-5 text-5xl mb-10" v-if="winner">
            <p>
                Congrats you win.
            </p>
        </div>

        <div class="mt-5" v-if="message">
            <p>
                {{ message }}
            </p>
        </div>

        <div class="flex flex-col mt-5" v-if="rolled_numbers && rolled_numbers.length > 0">
            <div class="grid grid-cols-10 gap-4 mx-2">
                <div class="" v-for="n in rolled_numbers">
                    <button class="bg-yellow-300 ml-2 text-black text-md rounded-full cursor-default"
                        style="height: 60px; width: 60px;"
                    >
                        {{ n }}
                    </button>
                </div>
            </div>
        </div>

        <div class="flex flex-col mt-5">
            <div class="grid grid-cols-3 gap-4 mx-2">
                <!-- CARD 1 -->
                <div class="bingo-card w-full flex flex-row">
                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            B
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="b in cards[0].b" :key="b.position"
                            @click="crossout('card_1', b.number, cards[0].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(b.number) && b.is_crossout }"
                        >
                            {{ b.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            I
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="i in cards[0].i" :key="i.position"
                            @click="crossout('card_1', i.number, cards[0].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(i.number) && i.is_crossout }"
                        >
                            {{ i.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            N
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="n in cards[0].n" :key="n.position"
                            @click="crossout('card_1', n.number, cards[0].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(n.number) && n.is_crossout }"
                        >
                            {{ n.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            G
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="g in cards[0].g" :key="g.position"
                            @click="crossout('card_1', g.number, cards[0].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(g.number) && g.is_crossout }"
                        >
                            {{ g.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            O
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="o in cards[0].o" :key="o.position"
                            @click="crossout('card_1', o.number, cards[0].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(o.number) && o.is_crossout }"
                        >
                            {{ o.number }}
                        </div>
                    </div>
                </div>
                
                <!-- CARD 2 -->
                <div class="bingo-card w-full flex flex-row">
                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            B
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="b in cards[1].b" :key="b.position"
                            @click="crossout('card_1', b.number, cards[1].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(b.number) && b.is_crossout }"
                        >
                            {{ b.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            I
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="i in cards[1].i" :key="i.position"
                            @click="crossout('card_1', i.number, cards[1].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(i.number) && i.is_crossout }"
                        >
                            {{ i.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            N
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="n in cards[1].n" :key="n.position"
                            @click="crossout('card_1', n.number, cards[1].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(n.number) && n.is_crossout }"
                        >
                            {{ n.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            G
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="g in cards[1].g" :key="g.position"
                            @click="crossout('card_1', g.number, cards[1].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(g.number) && g.is_crossout }"
                        >
                            {{ g.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            O
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="o in cards[1].o" :key="o.position"
                            @click="crossout('card_1', o.number, cards[1].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(o.number) && o.is_crossout }"
                        >
                            {{ o.number }}
                        </div>
                    </div>
                </div>

                <!-- CARD 3 -->
                <div class="bingo-card w-full flex flex-row">
                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            B
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="b in cards[2].b" :key="b.position"
                            @click="crossout('card_1', b.number, cards[2].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(b.number) && b.is_crossout }"
                        >
                            {{ b.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            I
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="i in cards[2].i" :key="i.position"
                            @click="crossout('card_1', i.number, cards[2].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(i.number) && i.is_crossout }"
                        >
                            {{ i.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            N
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="n in cards[2].n" :key="n.position"
                            @click="crossout('card_1', n.number, cards[2].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(n.number) && n.is_crossout }"
                        >
                            {{ n.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            G
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="g in cards[2].g" :key="g.position"
                            @click="crossout('card_1', g.number, cards[2].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(g.number) && g.is_crossout }"
                        >
                            {{ g.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            O
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="o in cards[2].o" :key="o.position"
                            @click="crossout('card_1', o.number, cards[2].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(o.number) && o.is_crossout }"
                        >
                            {{ o.number }}
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="flex flex-col mt-5">
            <div class="grid grid-cols-3 gap-4 mx-2">

                <!-- CARD 4 -->
                <div class="bingo-card w-full flex flex-row">
                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            B
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="b in cards[3].b" :key="b.position"
                            @click="crossout('card_1', b.number, cards[3].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(b.number) && b.is_crossout }"
                        >
                            {{ b.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            I
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="i in cards[3].i" :key="i.position"
                            @click="crossout('card_1', i.number, cards[3].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(i.number) && i.is_crossout }"
                        >
                            {{ i.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            N
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="n in cards[3].n" :key="n.position"
                            @click="crossout('card_1', n.number, cards[3].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(n.number) && n.is_crossout }"
                        >
                            {{ n.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            G
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="g in cards[3].g" :key="g.position"
                            @click="crossout('card_1', g.number, cards[3].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(g.number) && g.is_crossout }"
                        >
                            {{ g.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            O
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="o in cards[3].o" :key="o.position"
                            @click="crossout('card_1', o.number, cards[3].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(o.number) && o.is_crossout }"
                        >
                            {{ o.number }}
                        </div>
                    </div>
                </div>

                <!-- CARD 5 -->
                <div class="bingo-card w-full flex flex-row">
                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            B
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="b in cards[4].b" :key="b.position"
                            @click="crossout('card_1', b.number, cards[4].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(b.number) && b.is_crossout }"
                        >
                            {{ b.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            I
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="i in cards[4].i" :key="i.position"
                            @click="crossout('card_1', i.number, cards[4].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(i.number) && i.is_crossout }"
                        >
                            {{ i.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            N
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="n in cards[4].n" :key="n.position"
                            @click="crossout('card_1', n.number, cards[4].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(n.number) && n.is_crossout }"
                        >
                            {{ n.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            G
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="g in cards[4].g" :key="g.position"
                            @click="crossout('card_1', g.number, cards[4].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(g.number) && g.is_crossout }"
                        >
                            {{ g.number }}
                        </div>
                    </div>

                    <div class="w-full flex flex-col m-1">
                        <div class="w-full font-bold bingo-column-header flex justify-center items-center text-xl">
                            O
                        </div>

                        <div class="w-full font-bold bingo-number flex justify-center items-center"
                            v-for="o in cards[4].o" :key="o.position"
                            @click="crossout('card_1', o.number, cards[4].id)"
                            :class="{ 'bg-slate-400': rolled_numbers.includes(o.number) && o.is_crossout }"
                        >
                            {{ o.number }}
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            rolled_numbers: null,
            cards : null,
            rolled_letter: null,
            rolled_number: null,
            message: null,
            winner: false
        }
    },
    mounted(){
        this.getCards()
    },
    watch: {
        cards: {
            handler(val) {
                
                var card_1 = val[0]

                if(
                    card_1.b.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_1.i.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_1.n.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_1.g.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_1.o.filter( x => { return x.is_crossout == true }).length > 0 
                ) {
                    this.winner = true
                    this.finishTheGame()
                }

                var card_2 = val[1]

                if(
                    card_2.b.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_2.i.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_2.n.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_2.g.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_2.o.filter( x => { return x.is_crossout == true }).length > 0 
                ) {
                    this.winner = true
                    this.finishTheGame()
                }

                var card_3 = val[2]

                if(
                    card_3.b.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_3.i.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_3.n.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_3.g.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_3.o.filter( x => { return x.is_crossout == true }).length > 0 
                ) {
                    this.winner = true
                    this.finishTheGame()
                }

                var card_4 = val[3]

                if(
                    card_4.b.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_4.i.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_4.n.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_4.g.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_4.o.filter( x => { return x.is_crossout == true }).length > 0 
                ) {
                    this.winner = true
                    this.finishTheGame()
                }

                var card_5 = val[4]

                if(
                    card_5.b.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_5.i.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_5.n.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_5.g.filter( x => { return x.is_crossout == true }).length > 0 &&
                    card_5.o.filter( x => { return x.is_crossout == true }).length > 0 
                ) {
                    this.winner = true
                    this.finishTheGame()
                }

                
            },

            deep: true
        },
    },
    methods: {
        getCards() {
            var self = this

            axios.post('http://localhost:8000/api/bingo/cards', {})
                .then(function (response) {
                    self.rolled_numbers = response.data.data.rolled_numbers
                    self.cards = response.data.data.cards
                })
                .catch(function (error) {
                });
        },

        roll() {
            var self = this

            self.rolled_letter = null
            self.rolled_number = null

            axios.post('http://localhost:8000/api/bingo/roll-number', {})
                .then(function (response) {
                    self.rolled_numbers = response.data.data.game.rolled_numbers
                    self.rolled_letter = response.data.data.letter
                    self.rolled_number = response.data.data.number

                })
                .catch(function (error) {
                });
        },

        crossout(card_number, number, id) {
            var self = this

            self.message = null

            axios.post('http://localhost:8000/api/bingo/crossout-number', {card_number: card_number, number: number, id: id})
                .then(function (response) {
                    self.rolled_numbers = response.data.rolled_numbers
                    self.cards = response.data.cards
                })
                .catch(function (error) {
                    self.message = error.response.data

                    setTimeout(function() {
                        self.message = null
                    }, 3000)
                });

        },

        finishTheGame() {
            var self = this

            axios.post('http://localhost:8000/api/bingo/finish-game', {})
                .then(function (response) {
                    setTimeout(function() {
                        location.reload()
                    }, 5000)
                })
                .catch(function (error) {
                    
                });
        }
    }
}
</script>

<style scoped>
    .game-numbers {
        border: 1px solid black;
    }
    .bingo-card {
        border: 1px solid black;
    }

    .bingo-column-header {
        height: 100px;
        border: 1px solid black;
    }

    .bingo-number {
        height: 80px;
        border: 1px solid black;
        cursor: pointer;
    }
    
</style>