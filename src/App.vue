<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8 offset-md-2">
                <h3 class="text-center">Super quiz!</h3>
                <hr />
                <transition name="game" mode="out-in">
                    <possible-guesses
                            v-if="playing"
                            :addends="addends"
                            :choices="choices"></possible-guesses>
                    <end-game v-else></end-game>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    import { eventBus } from './main.js';
    import PossibleGuesses from './components/PossibleGuesses.vue';
    import EndGame from './components/EndGame.vue';

    export default {
        name: 'app',
        data() {
            return {
                range: 100,     // Addends will be in the interval [-range, range]
                addends: [],
                sum: null,
                choices: [],
                playing: true,
                max_addends: 2, // How many operands could the sum have?
                max_choices: 6  // How many choices should I offer, in total?
            }
        },
        methods: {
            newPair() {
                // Note: I know about Array.forEach, but this echoes in my mind when I use it: https://hackernoon.com/3-javascript-performance-mistakes-you-should-stop-doing-ebf84b9de951
                // (I can get a little obsessed sometimes about performance)

                // Fill choices array with bogus answers in random position
                this.choices = [];
                for (let i=0; i<this.max_choices-1; i++) {
                    this.choices.splice(Math.randInt(this.choices.length), 0, Math.randInt(this.range, -this.range));
                }

                // Create new sum
                this.addends = [];
                this.sum = 0;
                for (let i=0; i<this.max_addends; i++) {
                    this.addends[i] = Math.randInt(this.range) * Math.pow(-1, i);
                    this.sum += this.addends[i];
                }
                // Insert good answer in random position
                this.choices.splice(Math.randInt(this.choices.length), 0, this.sum);
                //console.log(this.sum); // No cheating! :P
            }
        },
        created() {
            // I will use random integers a lot so let's create a shortcut here
            Math.randInt = (max, min=0) => min + Math.ceil(Math.random() * max);

            // I'll use this reference inside the eventBus object
            const me = this;

            // A choice button was clicked
            eventBus.$on('choose', guess => {
                if (Number(guess) == this.sum) {
                    this.playing = false;
                } else {
                    alert('Oops, wrong answer!\nCare to try again? :)');
                }
            });

            // Start a new game
            eventBus.$on('newGame', function() {
                // In here *this* points to eventBus not the App's Vue object
                me.newPair();
                me.playing = true;
            });

            // At the beginning, start a new game :)
            eventBus.$emit('newGame');
        },
        components: {
            possibleGuesses: PossibleGuesses,
            endGame: EndGame
        }
    }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
    .game-enter-active, .game-leave-active {
        transition: all 0.2s ease-in-out;
    }
    .game-enter-to, .game-leave {
        transform: rotateY(0deg);
    }
    .game-enter, .game-leave-to {
        transform: rotateY(90deg);
    }
</style>