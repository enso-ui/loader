<template>
    <overlay :transparent="transparent"
        v-if="visible">
        <div class="loader"
            v-bind="$attrs"/>
    </overlay>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import Overlay from './Overlay.vue';

defineOptions({
    name: 'Loader',
    inheritAttrs: false,
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
    .overlay.is-overlay .loader {
        --enso-loader-outer-width: 3px;
        --enso-loader-middle-width: 2px;
        --enso-loader-inner-width: 1px;

        position: relative;
        margin: auto;
        box-sizing: border-box;
        width: 4em;
        height: 4em;
        border: 0;
        border-right: var(--enso-loader-outer-width) solid currentColor;
        border-radius: 50%;
        content: "";
        animation: enso-loader-spin-right 800ms linear infinite;

        &::before,
        &::after {
            content: "";
            position: absolute;
            display: block;
            box-sizing: border-box;
            border-radius: 50%;
        }

        &::before {
            inset: 12.5%;
            border: 0;
            border-left: var(--enso-loader-middle-width) solid currentColor;
            animation: enso-loader-spin-left 800ms linear infinite;
        }

        &::after {
            inset: 25%;
            border: 0;
            border-right: var(--enso-loader-inner-width) solid currentColor;
        }

        @each $color in "primary", "link", "info", "success", "warning", "danger", "light", "dark", "white", "black" {
            &.is-#{$color} {
                color: var(--bulma-#{$color});
            }
        }

        &.is-small {
            --enso-loader-outer-width: 2px;
            --enso-loader-middle-width: 1px;
            --enso-loader-inner-width: 1px;

            width: 3em;
            height: 3em;
        }

        &.is-medium {
            --enso-loader-outer-width: 4px;
            --enso-loader-middle-width: 3px;
            --enso-loader-inner-width: 2px;

            width: 5em;
            height: 5em;
        }

        &.is-large {
            --enso-loader-outer-width: 5px;
            --enso-loader-middle-width: 4px;
            --enso-loader-inner-width: 2px;

            width: 6em;
            height: 6em;
        }
    }

    @keyframes enso-loader-spin-left {
        from {
            transform: rotate(0deg);
        }

        to {
            transform: rotate(720deg);
        }
    }

    @keyframes enso-loader-spin-right {
        from {
            transform: rotate(360deg);
        }

        to {
            transform: rotate(0deg);
        }
    }
</style>
