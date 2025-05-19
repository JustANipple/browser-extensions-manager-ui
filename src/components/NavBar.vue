<script setup>
import { computed, onMounted, ref } from "vue";

const isLightTheme = ref(true);
if (window.matchMedia("(prefers-color-scheme: dark)").matches) {
    isLightTheme.value = false;
}

const imgUrl = computed(() => {
    return isLightTheme.value
        ? "/assets/images/logo.svg"
        : "/assets/images/logo-dark.svg";
});

const toggleTheme = () => {
    isLightTheme.value = !isLightTheme.value;
    document.documentElement.setAttribute(
        "data-theme",
        isLightTheme.value ? "light" : "dark"
    );
};

onMounted(() => {
    document.documentElement.setAttribute(
        "data-theme",
        isLightTheme.value ? "light" : "dark"
    );
});
</script>

<template>
    <Transition appear name="fade">
        <div
            class="navbar bg-primary drop-shadow drop-shadow-neutral rounded-xl px-3 py-0"
        >
            <div class="flex-1">
                <img :src="imgUrl" alt="Extensions" />
            </div>
            <div class="flex-none">
                <label
                    class="swap swap-rotate bg-neutral p-3 rounded-xl hover:bg-[#c6c6c6]"
                >
                    <input
                        type="checkbox"
                        class="theme-controller"
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
                        alt="moon icon"
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
