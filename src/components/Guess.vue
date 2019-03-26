<template>
    <button
            class="btn btn-primary"
            @click="eventBus.emit('choose', this.guess)"
        >{{ guess }}</button>
</template>

<script>
    import { eventBus } from '../App.vue';

    export default {
        props: ['guess']
    }
</script>