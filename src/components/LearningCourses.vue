<template>
    <div>
        <h2 class="mb-4">O'rganayotgan Darslar</h2>
        <div v-for="lesson in lessons" :key="lesson" class="lesson background_color">
            <span class="mr-5">{{ lesson }}</span>
            <button class="btn btn-outline-success" @click="$emit('complete', lesson)">Done</button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        lessons: {
            type: Array,
            required: true
        }
    }
};
</script>

<style>

span{
    font-size: 20px;
}

.background_color {
    background-color: transparent;
}


.lesson {
    margin: 10px 0;
    padding: 10px;
}
</style>