<template>
    <form @submit.prevent>
        <input v-model="inputValue" class="row" type="text" id="input-box">
        <button id="addBtn" class="btn" @click="createPost">Add Tasks</button>
    </form>
</template>

<script>
export default{
    data(){
        return{
            inputValue: ""
        }
    },
    methods:{
        createPost(){
            this.$emit('createNewPost', this.inputValue);
        }
    }
}
</script>


<style lang="scss">

form{
    display: flex;
    flex-direction: column;
    align-items: center;
    input{
        border: none;
        outline: none;

        width: 468px;
        padding: 10px;
        border-radius: 10px;

        background-color: #D9D9D9;

        margin-bottom: 15px;
    }
}

.btn{
    padding: 10px;
    width: 200px;
    margin-bottom: 35px;

    outline: none;
    border: none;

    border-radius: 10px;
    font-family: 'Racing Sans One', cursive;
    font-weight: 400;
    color: white;

    background-color: #4F4F4F;
    cursor: pointer;
}
</style>