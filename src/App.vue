<template>
	<div id="app">
		<the-header/>
		<router-view/>
		<the-footer/>
	</div>

</template>

<script>
    import TheHeader from './components/the-header.vue';
    import TheFooter from './components/the-footer.vue';

    export default {
        name: "app",
        components: {
            'the-header': TheHeader,
            'the-footer': TheFooter
        }
    }
</script>


<style lang="scss">
	@import 'scss/_common.scss';
</style>
