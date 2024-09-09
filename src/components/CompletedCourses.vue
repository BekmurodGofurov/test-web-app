<template>
    <div>
        <h2>Tugallangan Darslar</h2>
        <div v-for="lesson in lessons" :key="lesson" class="lesson">
            <h5>{{ lesson }}</h5>
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

h5{
    color: #cdd2e9;
}

.lesson {
    margin: 10px 0;
    padding: 10px;
}
</style>