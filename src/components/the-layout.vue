<template lang="pug">
	.container
		form.layout-container
			.layout.layout-left
				.layout-options
					.heading
						h2.h3 JS options:
						button.reset.hidden-print(
							type="reset"
							value="reset"
							@click="resetFields"
							) Res.
					ul.list.options-list
						li.options-item(
							v-for="(option, i) in optionsJS"
							:key="option.i"
							)
							the-check-box(
								v-model="option.status"
								) {{ option.name }}
			.layout.layout-center
				.components.unique-elemets
					.heading
						h2.h3 Unique el.:
						span.num-elements {{ uniqueElements }} el.
					label
						input.unique(
							type="number"
							placeholder="0"
							v-model.number="uniqueElements"
							@keypress="isNumber($event)"
							)
				.components.pages
					.heading
						h2.h3 Amount of Pages:
						span.num-elements {{ amountOfPages }}
					label
						input(
							type="number"
							placeholder="0"
							v-model.number="amountOfPages"
							@keypress="isNumber($event)"
							)
				.components.type
					.heading
						h2.h3 Layout Type:
					ul.list.types-list
						li.types-item(
							v-for="type in layoutTypes"
							)
							the-radio-button(
								v-model="layoutType"
								:time-calc="type.hour"
								) {{ type.name }}
				.components.requirements
					.heading
						h2.h3 Layout Requirements:
					ul.list.requirements-list
						li.requirements-item(
							v-for="requirement in requirements"
							)
							the-check-box(
								v-model="requirement.status"
								) {{ requirement.name }}
				.holder-notes
					.comments
						.heading
							h2.h3 Notes/Questions:
						label
							textarea.comments-item(
								type="text"
								placeholder="Enter your message"
								v-model="notes"
								)
					.final-result
						.extra
							.heading
								h2.h3 Extra Hours:
							label
								input(
									type="number"
									placeholder="0"
									@keypress="isNumber($event)"
									v-model="extraHours"
									)
						.days
							.heading
								h2.h3 Days: {{ (summary / 8).toFixed(2) }} d
						.hours
							.heading
								h2.h3 Hours: {{ summary }} h
			.layout.layout-right
				.summary
					h2.h3 Summary:
					.content
						.holder
							p Notes / Questions: {{ notes }}
						.holder
							p Extra Hours: {{ extraHours }} h.
						.holder
							p Days (8h/day): {{ (summary / 8).toFixed(2) }} d.
						.holder
							p Hours: {{ (summary).toFixed(2) }} h.
</template>

<script>
    import theCheckBox from './the-check-box.vue';
    import theRadioButton from './the-radio-button.vue';

    export default {
        name:	'TheLayout',
        components: {
            'the-check-box': theCheckBox,
            'the-radio-button': theRadioButton
        },
        data () {
            return {
                layoutType: 0,
                jsOption: [],
                layoutReq: [],



                isActive: true,
                amountOfPages: '',
                uniqueElements: '',
                notes: '',
                extraHours: '',

                optionsJS: [
                    { name: 'Carousel', 							hour: 2, 		status: false},
                    { name: 'Tabs', 								hour: 1, 		status: false},
                    { name: 'Accordion', 							hour: 3, 		status: false },
                    { name: 'Open Close',							hour: 21, 	status: false },
                    { name: 'Lightbox', 							hour: 15, 	status: false },
                    { name: 'Popup', 								hour: 0.3, 	status: false },
                    { name: 'Tooltip', 								hour: 3, 	status: false },
                    { name: 'Slider', 								hour: 2, 		status: false },
                    { name: 'Custom forms', 						hour: 2, 		status: false },
                    { name: 'Custom scroll', 						hour: 2, 		status: false },
                    { name: 'Animated sorting / Filter', 			hour: 2, 		status: false },
                    { name: 'Calendar / Datepicker', 				hour: 4, 		status: false },
                    { name: 'Form validation', 						hour: 1, 		status: false },
                    { name: 'Anchor navigation with smooth scroll', hour: 2, 		status: false },
                    { name: 'Masonry', 								hour: 2, 		status: false },
                    { name: 'Custom video player', 					hour: 2, 		status: false },
                    { name: 'Custom audio player', 					hour: 2, 		status: false },
                    { name: 'Background video', 					hour: 2, 		status: false },
                    { name: 'Parallax on background',				hour: 2, 		status: false },
                    { name: 'AJAX load more / Infinite scroll', 	hour: 2, 		status: false },
                    { name: 'Grid / List view switcher', 			hour: 2, 		status: false },
                    { name: 'Animation on scroll', 					hour: 2, 		status: false },
                    { name: 'Autocomplete', 						hour: 2, 		status: false },
                    { name: 'Preloader', 							hour: 2, 		status: false },
                ],
                layoutTypes: [
                    { name: 'Fixed / Flexible layout', 		hour: 2, status: false },
                    { name: 'Responsive at our discretion', hour: 3, status: false },
                    { name: '+ 1 Responsive Design', 		hour: 4, status: false },
                    { name: '+ 2 Responsive Designs', 		hour: 5, status: false },
                    { name: '+ 3 Responsive Designs', 		hour: 6, status: false },
                    { name: '+ 4 Responsive Designs', 		hour: 7, status: false }
                ],
                requirements: [
					{ name: 'Fonts (TypeKit, Fonts.com)', 	hour: 2, status: false },
                    { name: 'Footer at Bottom', 			hour: 2, status: false },
                    { name: 'Commented HTML/CSS', 			hour: 2, status: false },
                    { name: 'SSI Templates', 				hour: 2, status: false },
                    { name: 'WooCommerce WP minimum', 		hour: 2, status: false },
                    { name: 'WooCommerce WP medium', 		hour: 2, status: false },
                    { name: 'Markup for WordPress', 		hour: 2, status: false },
                    { name: 'Favicon', 						hour: 2, status: false },
                    { name: 'Retina', 						hour: 2, status: false },
                    { name: 'Twitter Bootstrap', 			hour: 2, status: false },
                    { name: 'Foundation Zurb', 				hour: 2, status: false },
                    { name: 'Materialize',					hour: 2, status: false },
                    { name: 'Print version CSS', 			hour: 2, status: false },
                    { name: 'Resizable Fonts', 				hour: 2, status: false }
				]
            }
        },
        methods: {
            isNumber: function(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
                    evt.preventDefault();
                } else {
                    return true;
                }
            },
            resetFields () {
                Object.assign(this.$data, this.$options.data.call(this));
            }
        },
        computed: {
            optionsJsResult() {
                let summ = 0;
                this.optionsJS.forEach((el)=> {
                    if(el.status) {
                        summ = summ + +el.hour
					}
				});
                return summ
			},
            requirementsResult() {
                let summ = 0;
                this.requirements.forEach((el)=> {
                    if(el.status) {
                        summ = summ + +el.hour
                    }
                });
                return summ
            },
			summary() {
                return 	this.optionsJsResult +
						this.requirementsResult +
						this.layoutType +
						this.uniqueElements*.5 +
						this.extraHours*1 +
						this.amountOfPages*1
			}
        },
    }
</script>

<style lang="scss" scoped>
	@import '../scss/_base.scss';

	.layout-container {
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		@include media('>widescreen') {
			flex-wrap: nowrap;
		}
	}

	.layout {
		margin: 0 5px;
		padding: 15px;
		border: 2px solid $color-text;
	}

	.layout-left,
	.layout-right {
		width: 100%;
		@include media('>widescreen') {
			width: 25%;
		}
	}

	.layout-left {
		margin-bottom: 15px;
		@include media('>tablet') {
			order: 0;
		}
		@include media('>widescreen') {
			width: 25%;
			margin-bottom: 0;
		}
	}

	.layout-center {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		width: 100%;
		min-height: 100%;
		margin-bottom: 15px;
		@include media('>widescreen') {
			width: 50%;
			margin-bottom: 0;
		}
	}

	.options-list {
		@include media('>skyline-phone') {
			column-count: 2;
		}
		@include media('>widescreen') {
			column-count: 1;
		}
	}

	.holder-notes {
		width: 100%;
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
	}

	.heading {
		display: flex;
		justify-content: space-between;
		align-items: flex-end;
		margin-bottom: 5px;
	}

	.h3 {
		margin-bottom: 0;
	}

	.reset {
		background: none;
		border: none;
		outline: none;
		color: $red;
		transition: color .3s;
		&:hover {
			color: $color-title;
		}
	}

	.num-elements {
		color: $color-title;
	}

	.components {
		width: 100%;
		padding-bottom: 15px;
		margin-bottom: 15px;
		border-bottom: 2px solid $bg-body;
	}

	.list {
		list-style-type: none;
		padding-left: 0;
		margin: 0;
	}

	.options-item {
		margin-bottom: 5px;
	}

	.type {
		display: flex;
		flex-wrap: wrap;
		flex-direction: column;
	}

	.types-list,
	.requirements-list {
		width: 100%;
		@include media('>skyline-phone') {
			column-count: 2;
		}

	}

	.types-item {
		display: flex;
		margin-bottom: 5px;
		-webkit-column-break-inside: avoid;
		break-inside: avoid;
	}

	.requirements-item {
		margin-bottom: 5px;
		-webkit-column-break-inside: avoid;
		break-inside: avoid;
	}

	.unique-elemets,
	.pages,
	.final-result,
	.comments {
		flex: 0 0 100%;
		@include media('>skyline-phone') {
			flex: 0 0 49%;
		}
	}

	.comments {
		label {
			display: block;
			margin-bottom: 15px;
			@include media('>skyline-phone') {
				margin-bottom: 0;
			}
		}
	}

	.extra {
		margin-bottom: 15px;
		@include media('>skyline-phone') {
			margin-bottom: 0;
		}
	}

	input,
	textarea {
		width: 100%;
		background: $bg-body;
		color: $bg-container;
	}

	.comments-item {
		min-height: 150px;
		resize: none;
	}

	.final-result {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.summary {
		.h3 {
			margin-bottom: 15px;
		}
		.holder {
			border-bottom: 2px dashed $bg-body;
			padding: 10px 0;
		}
		p {
			margin-bottom: 0;
		}
	}
</style>