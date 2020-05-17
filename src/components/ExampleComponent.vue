<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Example Component</div>

                    <div class="card-body">
                        <input type="text" v-model="email">

                        <button @click="login">Task 3</button>
                        <br>
                        <button @click="register">Register</button>
                        <br>
                        <button @click="resetPassword">Reset Password</button>
                        <button @click="updatePassword">Update PAssword</button>
                        <br>
                        <button @click="verifyEmail">Verify Email</button>
                        <br>
                        <button @click="getUser">THIS IS A HOT FIX</button>
                        <hr>
                        <template v-if="user">
                            Привет
                            <span v-text="user.name"></span>
                        </template>

                        <button @click="logout">Logout</button>
                    </div>
                </div>
            </div>
        </div>
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
                email: 'pavlikoksa@gmail.com'
            }
        },
        mounted() {
            console.log('Component mounted.')
        },

        methods: {
            login() {
                axios.get('/sanctum/csrf-cookie')
                    .then(response => {
                        axios.post('/moderator/auth/login', {
                            email: this.email,
                            password: 'password'
                        }).then(response => this.user = response.data.results
                        ).catch(err => console.log(err));
                    });

            },

            getUser() {
                axios.get('/moderator/user')
                    .then(response => {
                        this.user = response.data.results;
                    }).catch(err => console.log(err));
            },

            logout() {
                axios.post('/moderator/auth/logout')
                    .then(response => {
                        this.user = {};
                    }).catch(err => console.log(err));
            },

            register() {
                axios.get('/sanctum/csrf-cookie')
                    .then(response => {
                        axios.post('/auth/register', {
                            email: this.email,
                            password: 'password',
                            password_confirmation: 'password',
                            phone: '+7 (579) 355-17-30',
                            name: 'Ivan',
                            location_id: '04385137-9b6c-41e8-aeec-338f861f5d8e',
                            business_type: '1',
                            description: '222',
                            lead_count: '10',
                            planned_budget: '1',
                            personal_data: 1
                        }).then(response => this.user = response.data.results
                        ).catch(err => console.log(err));
                    });

            },

            resetPassword() {
                axios.get('/sanctum/csrf-cookie')
                    .then(response => {
                        axios.post('/auth/password/email', {
                            email: this.email,
                        }).then(response => console.log(response)
                        ).catch(err => console.log(err));
                    });
            },

            updatePassword() {
                axios.put('/moderator/moderators/daef7f95-ca84-4cea-8f42-1df9287952f6', {
                    password: 'password',
                    name: this.user.name,
                    email: this.user.email
                }).then(response => this.user = response.data.results
                ).catch(err => console.log(err));
            },

            verifyEmail() {
                axios.get('/email/verify/bb070328-9ee3-4c5a-a907-a2870baa71fe', {
                    params: {
                        expires: '1588937627',
                        signature: '58f7da11b9099e2ad994008808af92b978ffbbddf1ae0d23f1cf2c205785a2fd'
                    }
                })
                    .then(response => console.log(response))
                    .catch(err => console.log(err));
            }
        }
    }
</script>
