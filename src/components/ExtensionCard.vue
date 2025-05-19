<script setup>
const props = defineProps({
    logo: {
        type: String,
        required: true,
    },
    name: {
        type: String,
        required: true,
    },
    description: {
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
    <div
        class="bg-primary rounded-2xl p-5 flex flex-col justify-between h-[200px] border border-neutral md:basis-[380px]"
    >
        <div class="flex gap-4">
            <img :src="props.logo" :alt="props.name" class="h-15" />
            <div class="grid gap-y-2">
                <h2 class="font-bold text-xl">{{ props.name }}</h2>
                <p class="opacity-70 leading-5 tracking-tight">
                    {{ props.description }}
                </p>
            </div>
        </div>
        <div class="flex justify-between">
            <button
                class="btn bg-primary rounded-3xl shadow-sm text-primary-content border-neutral text-[16px]"
                @click="$emit('remove')"
            >
                Remove
            </button>
            <input
                type="checkbox"
                :checked="props.isActive"
                class="toggle toggle-sm bg-neutral checked:bg-accent checked:border-accent checked:text-accent-content my-auto"
            />
        </div>
    </div>
</template>
