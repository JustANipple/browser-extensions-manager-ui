<script setup>
import { computed, ref } from "vue";

const isLightTheme = ref(true);
const imgUrl = computed(() => {
    return isLightTheme.value
        ? "/assets/images/logo.svg"
        : "/assets/images/logo-dark.svg";
});

const toggleTheme = () => {
    isLightTheme.value = !isLightTheme.value;
};
</script>

<template>
    <Transition appear name="fade">
        <div
            class="navbar bg-primary drop-shadow-neutral rounded-xl px-2.5 py-0"
        >
            <div class="flex-1">
                <img :src="imgUrl" alt="Extensions" />
            </div>
            <div class="flex-none">
                <label class="swap swap-rotate bg-neutral p-3 rounded-xl">
                    <input
                        type="checkbox"
                        class="theme-controller"
                        value="dark"
                        :checked="!isLightTheme"
                        @change="toggleTheme"
                    />
                    <img
                        src="/assets/images/icon-sun.svg"
                        alt="sun icon"
                        class="swap-on"
                    />
                    <img
                        src="/assets/images/icon-moon.svg"
                        alt="moon icon icon"
                        class="swap-off"
                    />
                </label>
            </div>
        </div>
    </Transition>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s ease;
    transition-delay: 0.5s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
