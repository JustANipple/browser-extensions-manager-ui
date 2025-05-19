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
            class="btn shadow-sm px-5 py-[23px] rounded-3xl text-xl font-normal border-neutral cursor-pointer hover:opacity-60 focus:outline-accent"
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
