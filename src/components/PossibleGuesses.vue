<template>
    <div class="row">
        <div class="col-12">
            <div class="card text-center">
                <div class="card-header alert-secondary">
                    <h4>What is <span v-for="(addend, index) in addends">{{ addend > 0 && index ? '+': '' }}{{ addend }}</span> ?</h4>
                </div>
                <div class="row">
                    <div class="col-6 p-3" v-for="(choice, index) in choices">
                        <!-- class attribute changes to include 'btn-primary' on hovering over a button -->
                        <button
                                :class="[ 'btn', index == highlightedChoice ? 'btn-primary' : 'btn-text' ]"
                                @mouseover="highlightedChoice = index"
                                @mouseout="highlightedChoice = null"
                                @click="guessed(choice)">{{ choice }}</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { eventBus } from '../main.js';

    export default {
        data() {
            return {
                highlightedChoice: null
            }
        },
        props: {
            addends: Array,
            choices: Array
        },
        methods: {
            guessed: choice => { eventBus.$emit('choose', choice); }
        }
    }
</script>