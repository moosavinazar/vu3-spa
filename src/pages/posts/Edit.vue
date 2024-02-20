<template>
    <div v-if="pageLoading" class="spinner-border" role="status">
        <span class="visually-hidden">Loading...</span>
    </div>

    <div v-else class="col-md-6">
        <h2 class="mb-5">Update Post</h2>
        <PostForm @formData="updatePost" :button-loading="loading" button-text="Edit Post" :post="post"/>
    </div>
</template>

<script>
import PostForm from '@/components/posts/Form.vue'
import axios from 'axios';
import Swal from 'sweetalert2';
import { useRoute } from 'vue-router';
import { ref } from 'vue';
export default {
    components: {
        PostForm
    },
    setup() {
        const route = useRoute();
        const loading = ref(false);
        const post = ref({});
        const pageLoading = ref(true);

        function getPost() {
            axios
            .get(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
            .then(function (response) {
                // handle success
                post.value = response.data;
                pageLoading.value = false;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
        }

        getPost();

        function updatePost(formData) {
            loading.value = true;
            axios.put(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`, {
                id: route.params.id,
                title: formData.title,
                body: formData.body,
                userId: 1
            })
            .then(function () {
                // handle success
                loading.value = false;
                Swal.fire({
                    title: 'Thanks!',
                    text: 'Post udate successfully',
                    icon: 'success',
                    confirmButtonText: 'Ok'
                })
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
        }

        return {
            loading,
            updatePost,
            post,
            pageLoading
        }
    }
}
</script>

<style>

</style>