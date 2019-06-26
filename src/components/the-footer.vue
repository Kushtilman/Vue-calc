<template lang="pug">
	footer.footer
		.container
			p Here can be your advertising
			ul.function-list
				li.function-item(
					v-for="sending in sendings"
					:key="sending.id"
					)
					a.function-link(:href="`${sending.href}`")
						span(:class="`i ${sending.icon}`") {{ sending.name }}
</template>

<script>
    export default {
        name: 'TheFooter',
        data () {
            return {
                sendings: [
					{ icon: 'i-skype', 			href: 'skype:username?call',			name: '' },
                    { icon: 'i-telegram', 		href: 'tg://resolve?domain=<USERNAME>', name: '' },
                    { icon: 'i-mail-dot-ru', 	href: 'mailto:me@gmail.com',			name: '' },
                    { icon: 'print', 			href: '#',								name: 'print' }
				]
            }
        }
    }
</script>

<style lang="scss" scoped>
	@import '../scss/_base.scss';

	.footer {
		border-top: 2px solid $bg-body;
	}

	.container {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	p {
		margin-bottom: 0;
	}

	.function-list {
		display: flex;
		justify-content: flex-end;
		align-items: center;
		margin: 0;
		list-style-type: none;
		padding-left: 0;
	}

	.function-item {
		padding-left: 15px;
	}

	.function-link {
		text-decoration: none;
	}
	
	.i {
		color: $color-text;
		vertical-align: middle;
		transition: color .3s;
	}

	.i-skype {
		&:hover {
			color: $skype;
		}
	}

	.i-telegram {
		&:hover {
			color: $telegram;
		}
	}

	.i-mail-dot-ru {
		&:hover {
			color: $email;
		}
	}

	.screen,
	.print {
		&:hover {
			color: $white;
		}
	}
</style>