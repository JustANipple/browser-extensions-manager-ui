<script setup>
const props = defineProps({
    name: {
        type: String,
        required: true,
    },
    isActive: {
        type: Boolean,
        default: false,
    },
});
</script>

<template>
    <Transition appear name="fade">
        <button
            class="shadow-sm px-4.5 rounded-3xl text-xl font-normal border-neutral cursor-pointer"
            :class="{
                [isActive ? 'bg-accent text-accent-content' : 'bg-primary']:
                    true,
            }"
            @click="$emit('click')"
        >
            {{ name }}
        </button>
    </Transition>
</template>

<style scoepd>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
