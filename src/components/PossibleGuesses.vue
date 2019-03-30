<template>
    <div class="row">
        <div class="col-12">
            <div class="card text-center">
                <div class="card-header alert-secondary">
                    <h4>What is {{ numbers[0] }} {{ numbers[1] }} ?</h4>
                </div>
                <div class="row">
                    <div class="col-6 p-3" v-for="choice in choices">
                        <button
                                :class=""
                                @mouseover="">{{ choice }}</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { eventBus } from '../main.js';

    export default {
        props: {
            numbers: Array,
            choices: Array
        }
    }
</script>