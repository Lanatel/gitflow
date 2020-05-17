<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png">
        <ExampleComponent></ExampleComponent>
    </div>
</template>

<script>
    // @ is an alias to /src
    import HelloWorld from '@/components/HelloWorld.vue'
    import ExampleComponent from '@/components/ExampleComponent.vue'

    export default {
        name: 'Home',
        components: {
            HelloWorld,
            ExampleComponent
        },
    }
</script>
