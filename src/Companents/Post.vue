<template>
<div class="post" :class="{ active: post.status }">
    <label @click=updateCheckedStatus(post.id) class="custom-checkbox">
        <input type="checkbox" v-model="post.status">
    </label>
    <div class="postElement">{{ post.title }}</div>
    <button @click="deleteLi(post.id)" class="closeBtn"></button>
</div>
</template>

<script>
export default {
    props:{
        post:{
            type: Object,
            required: true 
        }
    }, 

    methods: {
        deleteLi(id) {
            this.$emit('delete', id);
        }, 

        updateCheckedStatus(id) {
            this.$emit('update-status', id);
        }
    }
}
</script>

<style scoped>
.post{
    width: 200px;
    display: flex;
    justify-content: space-between;
    color: white;
    align-items: center;
}

.custom-checkbox input[type="checkbox"] {
    -webkit-appearance: none;
    -moz-appearance: none;
    width: 20px; /* Ширина чекбокса */
    height: 20px; /* Высота чекбокса */
    border-radius: 50%; /* Скругление углов чекбокса */
    outline: none; /* Убираем контур при фокусе */
    cursor: pointer;
    border: 1px solid white;
}

.custom-checkbox input[type="checkbox"]:checked {
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8 8'%3e%3cpath fill='%23fff' d='M6.564.75l-3.59 3.612-1.538-1.55L0 4.26 2.974 7.25 8 2.193z'/%3e%3c/svg%3e");
    background-color: black;
}

.active {
    color: #555; /* Цвет текста */
    text-decoration: line-through; /* Зачеркивание текста */
}

.closeBtn{
    outline: none;
    border: none;

    width: 38px;
    height: 38px;
    background-image: url(./Trash.svg);
    background-size: contain;

    border-radius: 11px;
}
</style>