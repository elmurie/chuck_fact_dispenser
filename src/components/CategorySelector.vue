<template>
    <header>
        <ul class="container nav nav-pills d-flex flex-wrap">
            <li v-for="category in categories" :key="category" class="nav-item" @click="selectCategory(category)">
                <a href="#" class="nav-link text-capitalize" :class="{ active: category === selected }">{{ category }}</a>
            </li>
        </ul>
    </header>
</template>
  
<script>

export default {
    props: ['categories', 'selected'],
    emits: ['update:selected'],
    methods: {
        selectCategory(category) {
            if (category !== this.selected) {
                this.$emit('update:selected', category);
            }
        },
    },
};
</script>
  
<style>

header {
    width: 100%;
}

.nav-pills {
    justify-content: space-evenly;
}

.nav-link {
    color: white !important;
}

</style>
  