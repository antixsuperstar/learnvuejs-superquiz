<template>
    <div class="container">
        <div class="row">
            <div class="col-md-6 offset-md-3">
                <h3 class="text-center">Super quiz!</h3>
                <hr />
            </div>
        </div>
    </div>
</template>

<script>
    import Guess from './components/Guess.vue';

    export default {
        name: 'app',
        data() {
            return {
                intervals: [ -20, 20 ],
                numbers: []
            }
        },
        computed: {
            range: this.intervals[0] + this.intervals[1]
        },
        methods: {

        },
        created() {

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
