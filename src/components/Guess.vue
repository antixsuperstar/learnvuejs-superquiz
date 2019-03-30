<template>
    <button
            class="btn btn-primary"
            @click="eventBus.$emit('choose', this.guess)"
        >{{ guess }}</button>
</template>

<script>
    import { eventBus } from '../main.js';

    export default {
        props: ['guess']
    }
</script>