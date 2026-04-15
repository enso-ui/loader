<template>
    <component :is="component"
        v-bind="$attrs"/>
</template>

<script setup>
import { computed } from 'vue';
import Label from './skeletons/Label.vue';
import Chart from './skeletons/Chart.vue';
import Table from './skeletons/Table.vue';
import Form from './skeletons/Form.vue';

const components = {
    label: Label,
    chart: Chart,
    table: Table,
    form: Form,
};

defineOptions({
    name: 'Skeleton',
    inheritAttrs: false,
});

const props = defineProps({
    type: {
        type: String,
        required: true,
        validator: value => ['label', 'chart', 'table', 'form'].includes(value),
    },
});

const component = computed(() => components[props.type]);
</script>

<style lang="scss">
    .enso-skeleton {
        --enso-skeleton-base: color-mix(in srgb, var(--bulma-border) 80%, var(--bulma-scheme-main-bis));
        --enso-skeleton-glow: color-mix(in srgb, var(--bulma-scheme-main) 72%, transparent);

        position: relative;
        overflow: hidden;
        border-radius: inherit;

        &__line,
        &__circle,
        &__bar,
        &__donut,
        &__line-chart,
        &__point,
        &__table-cell,
        &__table-header-cell,
        &__field-label,
        &__field-input,
        &__button {
            position: relative;
            overflow: hidden;
            background: var(--enso-skeleton-base);
        }

        &__shine::after {
            content: '';
            position: absolute;
            inset: 0;
            transform: translateX(-100%);
            background: linear-gradient(90deg, transparent, var(--enso-skeleton-glow), transparent);
            animation: enso-skeleton-shimmer 1.35s ease-in-out infinite;
        }

        &__circle {
            width: 1rem;
            height: 1rem;
            border-radius: 999px;
            flex: 0 0 auto;

            &--sm {
                width: 0.9rem;
                height: 0.9rem;
            }
        }

        &__line {
            display: block;
            height: 0.7rem;
            border-radius: 999px;

            &--title {
                width: min(18rem, 48%);
                height: 0.85rem;
            }

            &--legend {
                width: 8rem;
            }

            &--legend-short {
                width: 3.5rem;
            }

            &--axis {
                width: 5.5rem;
                height: 0.55rem;
            }

            &--axis-short {
                width: 3.5rem;
                height: 0.55rem;
            }
        }
    }

    @keyframes enso-skeleton-shimmer {
        100% {
            transform: translateX(100%);
        }
    }
</style>
