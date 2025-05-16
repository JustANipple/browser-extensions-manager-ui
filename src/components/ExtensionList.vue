<script setup>
import { computed, ref } from "vue";
import ExtensionCard from "./ExtensionCard.vue";
import FilterButton from "./FilterButton.vue";
import rawData from "/src/data.json";

const activeButton = ref("All");
const buttonClicked = (string) => {
    activeButton.value = string;
};

const data = ref([...rawData]);
const datas = computed(() => {
    return data.value.filter((item) => {
        if (activeButton.value === "All") return true;
        if (activeButton.value === "Active") return item.isActive;
        if (activeButton.value === "Inactive") return !item.isActive;
        return true;
    });
});

function removeItem(itemToRemove) {
    data.value = data.value.filter((item) => item.name !== itemToRemove);
}
</script>

<template>
    <Transition appear name="fade">
        <section class="mt-10 grid gap-y-8">
            <div class="grid gap-y-5 md:flex md:justify-between align-middle">
                <h1 class="text-center text-4xl font-bold">Extension List</h1>
                <div class="flex justify-center gap-3">
                    <FilterButton
                        :name="'All'"
                        :isActive="activeButton === 'All'"
                        @click="buttonClicked('All')"
                    />
                    <FilterButton
                        :name="'Active'"
                        :isActive="activeButton === 'Active'"
                        @click="buttonClicked('Active')"
                    />
                    <FilterButton
                        :name="'Inactive'"
                        :isActive="activeButton === 'Inactive'"
                        @click="buttonClicked('Inactive')"
                    />
                </div>
            </div>

            <div>
                <TransitionGroup
                    appear
                    name="list"
                    tag="div"
                    class="grid gap-y-3 md:flex md:flex-wrap md:gap-3"
                >
                    <ExtensionCard
                        v-for="item in datas"
                        :key="item.name"
                        :logo="item.logo"
                        :name="item.name"
                        :description="item.description"
                        :isActive="item.isActive"
                        @remove="removeItem(item.name)"
                    />
                </TransitionGroup>
            </div>
        </section>
    </Transition>
</template>

<style scoped>
.list-move,
.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}

.list-leave-active {
    position: absolute;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s ease;
    transition-delay: 0.75s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
