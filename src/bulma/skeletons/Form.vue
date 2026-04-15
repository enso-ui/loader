<template>
    <div class="enso-skeleton enso-skeleton--form">
        <div class="enso-skeleton__form-section"
            v-for="section in sections"
            :key="`section-${section}`">
            <span class="enso-skeleton__line enso-skeleton__line--title enso-skeleton__shine"/>
            <div class="enso-skeleton__form-grid">
                <div class="enso-skeleton__field"
                    v-for="field in fieldsPerSection"
                    :key="`field-${section}-${field}`">
                    <span class="enso-skeleton__field-label enso-skeleton__shine"/>
                    <span class="enso-skeleton__field-input enso-skeleton__shine"/>
                </div>
            </div>
        </div>
        <div class="enso-skeleton__form-actions">
            <span class="enso-skeleton__button enso-skeleton__shine"/>
            <span class="enso-skeleton__button enso-skeleton__button--secondary enso-skeleton__shine"/>
        </div>
    </div>
</template>

<script setup>
defineOptions({
    name: 'FormSkeleton',
});

defineProps({
    fieldsPerSection: {
        type: Number,
        default: 4,
    },
    sections: {
        type: Number,
        default: 2,
    },
});
</script>

<style lang="scss">
    .enso-skeleton--form {
        display: grid;
        gap: 1.25rem;

        .enso-skeleton__form-section {
            display: grid;
            gap: 0.85rem;
        }

        .enso-skeleton__form-grid {
            display: grid;
            gap: 1rem;
            grid-template-columns: repeat(2, minmax(0, 1fr));
        }

        .enso-skeleton__field {
            display: grid;
            gap: 0.5rem;
        }

        .enso-skeleton__field-label {
            display: block;
            width: 6rem;
            height: 0.7rem;
            border-radius: 999px;
        }

        .enso-skeleton__field-input {
            display: block;
            height: 2.75rem;
            border-radius: var(--bulma-radius);
        }

        .enso-skeleton__form-actions {
            display: flex;
            justify-content: flex-end;
            gap: 0.75rem;
        }

        .enso-skeleton__button {
            width: 7rem;
            height: 2.5rem;
            border-radius: var(--bulma-radius);

            &--secondary {
                width: 5.5rem;
            }
        }
    }

    @media (max-width: 768px) {
        .enso-skeleton--form .enso-skeleton__form-grid {
            grid-template-columns: 1fr;
        }
    }
</style>
