<template>
    <div class="enso-skeleton enso-skeleton--label"
        :style="style">
        <span class="enso-skeleton__circle enso-skeleton__shine"
            v-if="icon"/>
        <span class="enso-skeleton__line enso-skeleton__line--title enso-skeleton__shine"/>
    </div>
</template>

<script setup>
import { computed } from 'vue';

defineOptions({
    name: 'LabelSkeleton',
});

const props = defineProps({
    icon: {
        type: Boolean,
        default: false,
    },
    width: {
        type: String,
        default: null,
    },
});

const style = computed(() => (props.width
    ? { width: props.width }
    : null));
</script>

<style lang="scss">
    .enso-skeleton--label {
        display: inline-flex;
        align-items: center;
        gap: 0.75rem;
        width: min(18rem, 48%);
        max-width: 100%;
    }
</style>
