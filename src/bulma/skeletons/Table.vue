<template>
    <div class="enso-skeleton enso-skeleton--table">
        <div class="enso-skeleton__toolbar">
            <span class="enso-skeleton__line enso-skeleton__line--legend enso-skeleton__shine"/>
            <span class="enso-skeleton__line enso-skeleton__line--legend-short enso-skeleton__shine"/>
        </div>
        <div class="enso-skeleton__table">
            <div class="enso-skeleton__table-head"
                :style="gridStyle">
                <span class="enso-skeleton__table-header-cell enso-skeleton__line enso-skeleton__shine"
                    v-for="column in columns"
                    :key="`head-${column}`"/>
            </div>
            <div class="enso-skeleton__table-row"
                :style="gridStyle"
                v-for="row in rows"
                :key="`row-${row}`">
                <span class="enso-skeleton__table-cell enso-skeleton__line enso-skeleton__shine"
                    v-for="column in columns"
                    :key="`cell-${row}-${column}`"/>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue';

defineOptions({
    name: 'TableSkeleton',
});

const props = defineProps({
    columns: {
        type: Number,
        default: 6,
    },
    rows: {
        type: Number,
        default: 10,
    },
});

const gridStyle = computed(() => ({
    gridTemplateColumns: `repeat(${props.columns}, minmax(0, 1fr))`,
}));
</script>

<style lang="scss">
    .enso-skeleton--table {
        display: grid;
        gap: 0.85rem;

        .enso-skeleton__toolbar {
            display: flex;
            justify-content: space-between;
            gap: 1rem;
        }

        .enso-skeleton__table {
            display: grid;
            gap: 0.6rem;
        }

        .enso-skeleton__table-head,
        .enso-skeleton__table-row {
            display: grid;
            align-items: center;
            gap: 0.75rem;
        }

        .enso-skeleton__table-header-cell {
            display: block;
            width: 72%;
            height: 0.72rem;
            border-radius: 999px;
        }

        .enso-skeleton__table-cell {
            display: block;
            width: 100%;
            max-width: 100%;
            height: 0.62rem;
            border-radius: 999px;
        }

        .enso-skeleton__table-row {
            min-height: 2.1rem;
            padding-block: 0.15rem;
        }

        .enso-skeleton__table-row .enso-skeleton__table-cell:nth-child(4n + 1) {
            width: 84%;
        }

        .enso-skeleton__table-row .enso-skeleton__table-cell:nth-child(4n + 2) {
            width: 62%;
        }

        .enso-skeleton__table-row .enso-skeleton__table-cell:nth-child(4n + 3) {
            width: 76%;
        }

        .enso-skeleton__table-row .enso-skeleton__table-cell:nth-child(4n + 4) {
            width: 54%;
        }
    }
</style>
