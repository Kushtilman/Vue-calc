<template lang="pug">
	main
		the-layout
</template>

<script>
    import theLayout from '../components/the-layout.vue';

    export default {
        name: "TheHome",
        components: {
            'the-layout': theLayout
        }
    }
</script>
