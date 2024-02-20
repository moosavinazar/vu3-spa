<template>
    <h2 class="mb-5">Create Post</h2>
    <div class="col-md-6">
        <PostForm @formData="createPost" :button-loading="loading" button-text="Create Post"/>
    </div>
</template>

<script>
import PostForm from '@/components/posts/Form.vue'
import { ref } from 'vue'
import axios from 'axios';
import Swal from 'sweetalert2';
export default {
    components: {
        PostForm
    },
    setup() {

        const loading = ref(false);

        function createPost(formData) {
            loading.value = true;
            axios.post('https://jsonplaceholder.typicode.com/posts', {
                title: formData.title,
                body: formData.body,
                userId: 1
            })
            .then(function () {
                // handle success
                loading.value = false;
                Swal.fire({
                    title: 'Thanks!',
                    text: 'Post cretaed successfully',
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
            createPost
        }
    }
}
</script>

<style>

</style>