<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-6">
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Explicabo, quasi pariatur? Quia, cum numquam animi dolores nam quae neque exercitationem perspiciatis eaque quo placeat voluptas mollitia officia. Repellat, ducimus nostrum?</p>
                <router-link class="btn btn-dark" :to="{name: 'users'}">Users</router-link>
                <router-link class="btn btn-light ms-3" :to="{name: 'posts'}">Posts</router-link>
            </div>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>

</style>