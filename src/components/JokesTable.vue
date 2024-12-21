<template>
    <div>
        <transition-group name="joke" tag="div" class="table" @before-leave="handleBeforeLeave">
            <div v-for="(joke, index) in jokes" :key="joke.id" class="joke-row"
                :style="{ animationDelay: index * 100 + 'ms' }">
                <div class="joke-item">{{ joke.value }}</div>
            </div>
        </transition-group>
    </div>
</template>

<script>
export default {
    props: ['jokes'],
    methods: {
        handleBeforeLeave(el) {
            el.style.display = 'none';
        },
    },
};
</script>

<style>
.table {
    width: 100%;
    margin-top: 1rem;
    border-collapse: collapse;
}

.joke-row {
    opacity: 0;
    transform: translateX(100%);
    animation: slideIn 0.5s ease forwards;
    background: purple;
    color: white;
    border-radius: 5px;
}

.joke-item {
    min-height: 50px;
    padding: 5px 10px;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
}

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateX(100%);
    }

    to {
        opacity: 1;
        transform: translateX(0);
    }
}

.joke-leave-active {
    opacity: 0 !important;
    transform: translateX(100%) !important;
    transition: none !important;
}
</style>
