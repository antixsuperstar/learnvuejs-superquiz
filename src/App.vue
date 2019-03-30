<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8 offset-md-2">
                <h3 class="text-center">Super quiz!</h3>
                <hr />
                <possible-guesses
                        :numbers="numbers"
                        :choices="choices"></possible-guesses>
                <end-game></end-game>
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
                range: 100,
                numbers: [],
                choices: [1,2,3],
                playing: true
            }
        },
        methods: {
            newPair() {
                for (let i = 0; i<2; i++) {
                    this.numbers[i] = Math.floor(Math.random() * this.range * Math.pow(-1, i));
                }
                this.logPairs();
            },
            logPairs() {
                console.log(this.numbers);
            }
        },
        created() {
            this.newPair();

            eventBus.$on('choose', guess => {

            });
            eventBus.$on('newGame', function() {
                console.log(this);
                this.newPair();
                this.playing = true;
            });
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
</style>