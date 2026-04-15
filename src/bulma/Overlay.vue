<template>
    <fade>
        <div class="overlay is-overlay"
            :class="{ 'is-opaque': !transparent }"
            v-if="visible">
            <slot/>
        </div>
    </fade>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { Fade } from '@enso-ui/transitions';

defineOptions({
    name: 'Overlay',
});

defineProps({
    transparent: {
        type: Boolean,
        default: false,
    },
});

const visible = ref(false);

onMounted(() => {
    visible.value = true;
});
</script>

<style lang="scss">
    .overlay.is-overlay {
        display: flex;
        border-radius: inherit;

        &.is-opaque {
            background: rgba(255, 255, 255, 0.5);
        }
    }
</style>
