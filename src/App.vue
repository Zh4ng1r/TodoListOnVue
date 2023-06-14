<template class="template">
<div class="app container">
    <div class="todoApp">
        <h1>To-Do Now</h1>
        <Postform @createNewPost="createPosts"/>
        <Post v-for="post in posts" :post="post" :key="post.id" @delete="deleteLi" @update-status="updateCheckedStatus"/>
    </div>
</div>
</template>

<script>
import Postform from './Companents/Postform.vue'
import Post from './Companents/Post.vue'
export default{
    components:{
       Postform, Post
    },
    data(){
        return {
            posts: [
                {id: 1, title: 'Hello world', status:false},
            ],
        }
    },
    mounted() {
        this.loadInformation();
    },

    methods: {
        createPosts(inputValue) {
            const newPost = {
                id: Date.now(),
                title: inputValue,
                status: false
            }
            this.posts.push(newPost);
            this.saveInformation()
        },

        deleteLi(id){
            this.posts = this.posts.filter(post => post.id !== id);
            this.saveInformation()
        },

        updateCheckedStatus(id) {
            const post = this.posts.find(post => post.id === id);
            if(post.status === false){
                post.status = true;
            } else {
                post.status = false;
            }
            this.saveInformation()
        },

        saveInformation(){
            let todoListStringify = JSON.stringify(this.posts);
            localStorage.setItem('toDoList', todoListStringify);
        },

        loadInformation() {
            const todoListStringify = localStorage.getItem('toDoList');
            if(todoListStringify){
                this.posts = JSON.parse(todoListStringify);
            }
        }
        
    }
}      
</script>

<style lang="scss" scoped>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.container{
    width: 100%;
    height: 100vh;
    background-color: #2C2C2C;
}

.todoApp{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

h1{
    font-family: 'Racing Sans One', cursive;
    font-size: 64px;
    color: white;

    text-transform: uppercase;

    padding: 53px;
    margin-bottom: 30px;

    border-bottom: 1px solid white;
}
</style>