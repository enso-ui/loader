<template>
    <div class="enso-skeleton enso-skeleton--chart">
        <div class="enso-skeleton__legend">
            <span class="enso-skeleton__line enso-skeleton__line--legend-short enso-skeleton__shine"/>
            <span class="enso-skeleton__line enso-skeleton__line--legend enso-skeleton__shine"/>
        </div>
        <div class="enso-skeleton__chart-surface"
            :style="surfaceStyle">
            <template v-if="resolvedVariant === 'donut'">
                <span class="enso-skeleton__donut enso-skeleton__shine"/>
            </template>
            <template v-else-if="resolvedVariant === 'pie'">
                <span class="enso-skeleton__pie enso-skeleton__shine"/>
            </template>
            <template v-else-if="resolvedVariant === 'polar'">
                <span class="enso-skeleton__polar-slice enso-skeleton__polar-slice--1 enso-skeleton__shine"/>
                <span class="enso-skeleton__polar-slice enso-skeleton__polar-slice--2 enso-skeleton__shine"/>
                <span class="enso-skeleton__polar-slice enso-skeleton__polar-slice--3 enso-skeleton__shine"/>
                <span class="enso-skeleton__polar-slice enso-skeleton__polar-slice--4 enso-skeleton__shine"/>
            </template>
            <template v-else-if="resolvedVariant === 'radar'">
                <span class="enso-skeleton__radar-grid"/>
                <span class="enso-skeleton__radar-shape enso-skeleton__shine"/>
                <span class="enso-skeleton__radar-point enso-skeleton__radar-point--1 enso-skeleton__shine"/>
                <span class="enso-skeleton__radar-point enso-skeleton__radar-point--2 enso-skeleton__shine"/>
                <span class="enso-skeleton__radar-point enso-skeleton__radar-point--3 enso-skeleton__shine"/>
                <span class="enso-skeleton__radar-point enso-skeleton__radar-point--4 enso-skeleton__shine"/>
                <span class="enso-skeleton__radar-point enso-skeleton__radar-point--5 enso-skeleton__shine"/>
            </template>
            <template v-else-if="resolvedVariant === 'bubble'">
                <span class="enso-skeleton__bubble enso-skeleton__bubble--1 enso-skeleton__shine"/>
                <span class="enso-skeleton__bubble enso-skeleton__bubble--2 enso-skeleton__shine"/>
                <span class="enso-skeleton__bubble enso-skeleton__bubble--3 enso-skeleton__shine"/>
                <span class="enso-skeleton__bubble enso-skeleton__bubble--4 enso-skeleton__shine"/>
                <span class="enso-skeleton__bubble enso-skeleton__bubble--5 enso-skeleton__shine"/>
            </template>
            <template v-else-if="resolvedVariant === 'circles'">
                <span class="enso-skeleton__stacked-circle enso-skeleton__stacked-circle--1 enso-skeleton__shine"/>
                <span class="enso-skeleton__stacked-circle enso-skeleton__stacked-circle--2 enso-skeleton__shine"/>
                <span class="enso-skeleton__stacked-circle enso-skeleton__stacked-circle--3 enso-skeleton__shine"/>
            </template>
            <template v-else-if="resolvedVariant === 'line'">
                <span class="enso-skeleton__line-chart enso-skeleton__shine"/>
                <span class="enso-skeleton__point enso-skeleton__point--1 enso-skeleton__shine"/>
                <span class="enso-skeleton__point enso-skeleton__point--2 enso-skeleton__shine"/>
                <span class="enso-skeleton__point enso-skeleton__point--3 enso-skeleton__shine"/>
                <span class="enso-skeleton__point enso-skeleton__point--4 enso-skeleton__shine"/>
                <span class="enso-skeleton__point enso-skeleton__point--5 enso-skeleton__shine"/>
            </template>
            <template v-else>
                <span class="enso-skeleton__bar enso-skeleton__bar--1 enso-skeleton__shine"/>
                <span class="enso-skeleton__bar enso-skeleton__bar--2 enso-skeleton__shine"/>
                <span class="enso-skeleton__bar enso-skeleton__bar--3 enso-skeleton__shine"/>
                <span class="enso-skeleton__bar enso-skeleton__bar--4 enso-skeleton__shine"/>
                <span class="enso-skeleton__bar enso-skeleton__bar--5 enso-skeleton__shine"/>
                <span class="enso-skeleton__bar enso-skeleton__bar--6 enso-skeleton__shine"/>
            </template>
        </div>
        <div class="enso-skeleton__axis">
            <span class="enso-skeleton__line enso-skeleton__line--axis-short enso-skeleton__shine"/>
            <span class="enso-skeleton__line enso-skeleton__line--axis enso-skeleton__shine"/>
            <span class="enso-skeleton__line enso-skeleton__line--axis-short enso-skeleton__shine"/>
            <span class="enso-skeleton__line enso-skeleton__line--axis enso-skeleton__shine"/>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue';

defineOptions({
    name: 'ChartSkeleton',
});

const props = defineProps({
    aspectRatio: {
        type: [Number, String],
        default: '16 / 9',
    },
    variant: {
        type: String,
        default: 'generic',
        validator: value => [
            'generic',
            'chart',
            'bar',
            'horizontalBar',
            'line',
            'bubble',
            'circles',
            'doughnut',
            'donut',
            'pie',
            'polar',
            'polarArea',
            'radar',
        ].includes(value),
    },
});

const resolvedVariant = computed(() => {
    switch (props.variant) {
    case 'bar':
    case 'horizontalBar':
        return 'bar';
    case 'line':
    case 'chart':
        return 'line';
    case 'bubble':
        return 'bubble';
    case 'circles':
        return 'circles';
    case 'doughnut':
    case 'donut':
        return 'donut';
    case 'pie':
        return 'pie';
    case 'polar':
    case 'polarArea':
        return 'polar';
    case 'radar':
        return 'radar';
    default:
        return 'bar';
    }
});

const surfaceStyle = computed(() => ({
    aspectRatio: `${props.aspectRatio}`,
}));
</script>

<style lang="scss">
    .enso-skeleton--chart {
        display: grid;
        gap: 1rem;

        .enso-skeleton__legend,
        .enso-skeleton__axis {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .enso-skeleton__chart-surface {
            position: relative;
            display: grid;
            align-items: end;
            grid-template-columns: repeat(6, minmax(0, 1fr));
            gap: 0.85rem;
            min-height: 13rem;
            padding: 1rem 0.35rem 0.75rem;
            border-radius: var(--bulma-radius-large);
            background:
                linear-gradient(to top, color-mix(in srgb, var(--bulma-border) 60%, transparent) 1px, transparent 1px) 0 100% / 100% 25% repeat-y;
        }

        .enso-skeleton__bar {
            display: block;
            border-radius: 999px 999px 0 0;
            min-height: 2.5rem;

            &--1 { height: 42%; }
            &--2 { height: 64%; }
            &--3 { height: 83%; }
            &--4 { height: 56%; }
            &--5 { height: 72%; }
            &--6 { height: 34%; }
        }

        .enso-skeleton__line-chart {
            position: absolute;
            inset: 18% 8% 16% 8%;
            clip-path: polygon(0% 76%, 18% 58%, 36% 67%, 54% 34%, 72% 44%, 100% 12%, 100% 28%, 72% 56%, 54% 46%, 36% 79%, 18% 70%, 0% 88%);
            border-radius: 0.5rem;
        }

        .enso-skeleton__point {
            position: absolute;
            width: 0.75rem;
            height: 0.75rem;
            border-radius: 999px;

            &--1 { left: 9%; top: 61%; }
            &--2 { left: 26%; top: 47%; }
            &--3 { left: 44%; top: 56%; }
            &--4 { left: 62%; top: 27%; }
            &--5 { left: 89%; top: 8%; }
        }

        .enso-skeleton__donut {
            position: absolute;
            inset: 10% 26%;
            border-radius: 999px;
            background:
                radial-gradient(circle at center,
                    transparent 0 38%,
                    color-mix(in srgb, var(--bulma-scheme-main-bis) 100%, transparent) 39% 48%,
                    transparent 49%),
                conic-gradient(
                    color-mix(in srgb, var(--bulma-border) 85%, var(--bulma-scheme-main-bis)) 0 22%,
                    color-mix(in srgb, var(--bulma-primary) 24%, var(--bulma-scheme-main-bis)) 22% 51%,
                    color-mix(in srgb, var(--bulma-info) 18%, var(--bulma-scheme-main-bis)) 51% 76%,
                    color-mix(in srgb, var(--bulma-success) 18%, var(--bulma-scheme-main-bis)) 76% 100%
                );
        }

        .enso-skeleton__pie {
            position: absolute;
            inset: 10% 26%;
            border-radius: 999px;
            background: conic-gradient(
                color-mix(in srgb, var(--bulma-border) 85%, var(--bulma-scheme-main-bis)) 0 26%,
                color-mix(in srgb, var(--bulma-primary) 24%, var(--bulma-scheme-main-bis)) 26% 54%,
                color-mix(in srgb, var(--bulma-info) 18%, var(--bulma-scheme-main-bis)) 54% 78%,
                color-mix(in srgb, var(--bulma-success) 18%, var(--bulma-scheme-main-bis)) 78% 100%
            );
        }

        .enso-skeleton__polar-slice {
            position: absolute;
            inset: 14% 22%;
            border-radius: 999px;
            background:
                radial-gradient(circle at center,
                    transparent 0 26%,
                    color-mix(in srgb, var(--bulma-border) 78%, var(--bulma-scheme-main-bis)) 27% 100%);

            &--1 { clip-path: polygon(50% 50%, 76% 0%, 100% 30%, 68% 56%); }
            &--2 { inset: 18% 26%; clip-path: polygon(50% 50%, 100% 32%, 88% 100%, 54% 67%); }
            &--3 { inset: 10% 18%; clip-path: polygon(50% 50%, 46% 68%, 0% 100%, 0% 34%); }
            &--4 { inset: 22% 30%; clip-path: polygon(50% 50%, 32% 42%, 0% 0%, 66% 0%); }
        }

        .enso-skeleton__radar-grid {
            position: absolute;
            inset: 13% 20%;
            border-radius: 999px;
            background:
                radial-gradient(circle at center,
                    transparent 0 22%,
                    color-mix(in srgb, var(--bulma-border) 52%, transparent) 22.5% 23.5%,
                    transparent 24% 44%,
                    color-mix(in srgb, var(--bulma-border) 52%, transparent) 44.5% 45.5%,
                    transparent 46% 66%,
                    color-mix(in srgb, var(--bulma-border) 52%, transparent) 66.5% 67.5%,
                    transparent 68%),
                linear-gradient(color-mix(in srgb, var(--bulma-border) 42%, transparent), color-mix(in srgb, var(--bulma-border) 42%, transparent)) center / 1px 100% no-repeat,
                linear-gradient(90deg, color-mix(in srgb, var(--bulma-border) 42%, transparent), color-mix(in srgb, var(--bulma-border) 42%, transparent)) center / 100% 1px no-repeat;
        }

        .enso-skeleton__radar-shape {
            position: absolute;
            inset: 21% 26%;
            clip-path: polygon(50% 0%, 100% 32%, 82% 100%, 20% 86%, 0% 30%);
            border-radius: 1rem;
        }

        .enso-skeleton__radar-point {
            position: absolute;
            width: 0.75rem;
            height: 0.75rem;
            border-radius: 999px;

            &--1 { left: 48%; top: 17%; }
            &--2 { left: 73%; top: 34%; }
            &--3 { left: 67%; top: 78%; }
            &--4 { left: 26%; top: 67%; }
            &--5 { left: 16%; top: 34%; }
        }

        .enso-skeleton__bubble {
            position: absolute;
            border-radius: 999px;

            &--1 {
                width: 2.25rem;
                height: 2.25rem;
                left: 12%;
                top: 58%;
            }

            &--2 {
                width: 3rem;
                height: 3rem;
                left: 28%;
                top: 31%;
            }

            &--3 {
                width: 1.85rem;
                height: 1.85rem;
                left: 49%;
                top: 47%;
            }

            &--4 {
                width: 3.5rem;
                height: 3.5rem;
                left: 63%;
                top: 19%;
            }

            &--5 {
                width: 2.5rem;
                height: 2.5rem;
                left: 82%;
                top: 63%;
            }
        }

        .enso-skeleton__stacked-circle {
            position: absolute;
            border-radius: 999px;

            &--1 {
                inset: 21% 39% 21% 17%;
            }

            &--2 {
                inset: 16% 18% 16% 40%;
            }

            &--3 {
                inset: 33% 29% 8% 29%;
            }
        }
    }
</style>
