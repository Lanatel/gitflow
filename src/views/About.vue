<template>
    <div class="about">
        <h1>This is a user page</h1>

        <span v-text="user.name"></span><br>
        <span v-text="user.email"></span><br>
        <span v-text="user.balance"></span><br>
    </div>
</template>

<script>

    import axios from 'axios';

    axios.defaults.withCredentials = true;
    axios.defaults.baseURL = 'http://localhost:8003';

    export default {


        data() {
            return {
                user: {},
            }

        },
        mounted() {
            axios.get('/moderator/user').then(response => {
                this.user = response.data.results;
            }).catch(err => console.log(err));
        }
    }

</script>
