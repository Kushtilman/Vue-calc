<template lang="pug">
	label.btn-radio
		input(
			type="radio"
			name="radio-btn"
			:value="timeCalc"
			v-model="radioButtonValue"
			)
		svg(width='20px', height='20px', viewBox='0 0 20 20')
			circle(cx='10', cy='10', r='9')
			path.inner(d='M10,7 C8.34314575,7 7,8.34314575 7,10 C7,11.6568542 8.34314575,13 10,13 C11.6568542,13 13,11.6568542 13,10 C13,8.34314575 11.6568542,7 10,7 Z')
			path.outer(d='M10,1 L10,1 L10,1 C14.9705627,1 19,5.02943725 19,10 L19,10 L19,10 C19,14.9705627 14.9705627,19 10,19 L10,19 L10,19 C5.02943725,19 1,14.9705627 1,10 L1,10 L1,10 C1,5.02943725 5.02943725,1 10,1 L10,1 Z')
		span.radio-title
			slot
</template>

<script>
    export default {
        name: 'TheRadioButton',
        props: {
            value: [Boolean, String, Number],
            timeCalc: Number
        },
        computed: {
            radioButtonValue: {
                get: function() {
                    return this.value
                },
                set: function() {
                    // Communicate the change to parent component so that selectedValue can be updated
                    this.$emit("input", this.timeCalc)
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
	@import '../scss/_base.scss';

	.btn-radio {
		cursor: pointer;
		display: inline-block;
		float: left;
		-webkit-user-select: none;
		user-select: none;
		@media screen and (max-width: 480px) {
			display: block;
			float: none;
			&:not(:first-child) {
				margin-left: 0;
				margin-top: 15px;
			}
		}
		&:hover {
			.radio-title {
				color: $color-title;
			}
			svg {
				.outer {
					stroke-dasharray: 0;
				}
			}
		}
		svg {
			fill: none;
			vertical-align: middle;
			margin-right: 10px;
			circle {
				stroke-width: 2;
				stroke: $bg-body;
			}
			path {
				stroke: $color-title;
				&.inner {
					stroke-width: 6;
					stroke-dasharray: 19;
					stroke-dashoffset: 19;
				}
				&.outer {
					stroke-width: 2;
					stroke-dasharray: 57;
					stroke-dashoffset: 57;
					transition: fill .3s;
				}
			}
		}
		input {
			display: none;
			&:checked + svg {
				path {
					transition: all .4s ease;
					&.inner {
						stroke-dashoffset: 38;
					}
					&.outer {
						stroke-dashoffset: 0;
					}
				}
			}
			&:checked ~ .radio-title {
				color: $color-title;
			}
		}
	}

	.radio-title {
		display: contents;
		line-height: 1.4;
		vertical-align: middle;
		transition: color .3s;
	}
</style>