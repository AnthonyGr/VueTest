<template>
    <div class="wrapper">
        
        <h1>Страница с постами</h1>
        
        <MyInput
            placeholder="Поиск"
            v-model="searchQuery"
            
        />
        
        <div class="app__btns">
            <Button @click="showDialog">Создать пост</Button>
            <MySelect
              v-model="selectedSort"
              :options="sortOptions"
            />
        </div>
        <MyDialog v-model:show="dialogVisible">
            <PostForm @create="createPost"/>
        </MyDialog>
        <p v-if="isPostLoading === true">Идет загрузка...</p>
        <PostList v-if="isPostLoading === false" :posts="sortedAndSearchedPosts" @remove="removePost"/>
    
    </div>
</template>

<script>
import PostForm from "./components/PostForm";
import PostList from "./components/PostList";
import MyDialog from "@/components/UI/MyDialog";
import Button from "@/components/UI/Button";
import MySelect from "@/components/UI/MySelect";
import MyInput from "@/components/UI/MyInput";

export default {
    components: {MyInput, MySelect, Button, MyDialog, PostForm, PostList},
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostLoading: true,
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержимому'},
            ],
            searchQuery: '',
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id);
        },
        showDialog() {
            this.dialogVisible = true
        },
        async fetchPosts() {
            try {
                this.isPostLoading = true
                const res = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=5');
                this.posts = await res.json();
            } catch (e) {
                alert('Ошибка')
            } finally {
                this.isPostLoading = false
            }
        },
    },
    mounted() {
        this.fetchPosts()
    },
    computed: {
      sortedPosts() {
          return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
      },
        sortedAndSearchedPosts() {
          return this.sortedPosts.filter(post => post.title.includes(this.searchQuery))
        }
    },
    // watch:  {
    //     selectedSort(newValue) {
    //         this.posts.sort((post1, post2) => {
    //             return post1[this.selectedSort]?.localeCompare(post2[newValue])
    //         })
    //     }
    // }
};
</script>

<style lang="sass" scoped>


.wrapper
    max-width: 800px
    padding: 30px 20px
    margin: 0 auto

.app__btns
    display: flex
    justify-content: space-between
</style>
