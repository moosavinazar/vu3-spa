<template>
    <div v-if="loading" class="spinner-border" role="status">
        <span class="visually-hidden">Loading...</span>
    </div>
    <div v-else class="col-md-5">
        <div class="card">
            <div class="card-header">
                {{ post.title }}
            </div>
            <ul class="list-group list-group-flush">
                <li class="list-group-item">{{ post.body }}</li>
            </ul>
            <div class="card-footer">
                <button @click="deletePost" class="btn btn-sm btn-danger me-4">Delete</button>
                <router-link class="btn btn-sm btn-dark" :to="{ name:'editPost', params:{id: post.id} }">Edit</router-link>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import Swal from 'sweetalert2';
import { ref } from 'vue';
import { useRoute } from 'vue-router';

export default {
    setup() {
        const post = ref({});
        const loading = ref(true)
        const route = useRoute();

        function getPost() {
            axios
            .get(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
            .then(function (response) {
                // handle success
                post.value = response.data;
                loading.value = false;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
        }

        getPost();

        function deletePost() {
            axios
            .delete(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
            .then(function () {
                Swal.fire({
                    title: 'Thanks!',
                    text: `Post (${route.params.id}) delete successfully`,
                    icon: 'warning',
                    confirmButtonText: 'Ok'
                })
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
        }

        return{
            post,
            loading,
            route,
            deletePost
        }
    }
}
</script>

<style>

</style>