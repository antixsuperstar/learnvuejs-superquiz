<template>
    <div class="row">
        <div class="col-12">
            <div class="card alert-success text-center p-3">
                <h4>That's correct!</h4>
                <hr />
                <button
                        class="btn btn-primary col-4 offset-4"
                        @click="restartGame">Next Question</button>
            </div>
        </div>
    </div>
</template>

<script>
    import { eventBus } from '../main.js';

    export default {
        props: [
            'justFinishedGame'
        ],
        methods: {
            restartGame: () => { eventBus.$emit('newGame'); }
        }
    }
</script>