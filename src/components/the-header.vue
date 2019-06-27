<template lang="pug">
	header.header.hidden-print
		.container
			.logo
				a(href="https://www.ssa.group/")
					img(src="../assets/logo.png" alt="SSA Group")
			ul.navbar
				button.navbar-item(
					type="button"
					@click="crossEstimation"
					)
					span.i.i-book1
					| How it works
				button.navbar-item(
					type="button"
					@click="crossTutorial"
					)
					span.i.i-params
					| Tutorial
			transition(name="slide-fade")
				.estimation(
					v-show="isActive"
					name="Estimation"
					)
					button.close-btn(
						type="button"
						@click="closeTutorial"
						)
						span.i.i-cross
					.text-holder
						h1.h2 Много текста о том как этим пользоваться, примеры...
						h2.h3 Правила и принципы поэлементной оценки markup duration проекта
						p Данный подход к оцениванию трудозатрат на проект (duration) основывается на том, что больше всего времени разработчик тратит на порезку и стилизацию элементов дизайна.
						p Основная цель данного подхода, это дать компании инструмент, с помощью которого можно обеспечить прозрачность и понятность оценки для проекта любой специфики и сложности.
						h3.h3 Процесс оценивания
						p Для того, чтобы сделать оценку проекта, разработчику необходимо посчитать количество уникальных элементов в дизайнах и перевести их в рабочие часы с помощью калькулятора. Для этого разработчик может воспользоваться одним из двух вариантов:
						ul.estimation-list
							li.estimation-item Посчитать элементы можно используя например Photoshop, создав свою папку в слоях выше всех, и используя инструмент 'Прямоугольник' выделять элементы example. Затем посчитанные элементы и доп опции переводятся в рабочий часы в калькуляторе. Гайд по работе с этим калькулятором смотрите здесь.
							li.estimation-item Estimator - tool, который позволяет произвести разметку и калькуляцию duration сразу в одном месте. Гайд по использованию данного тула смотрите здесь.
						blockquote.estimation-blockquote
							h4.h4 Важно
							p Все принципы рассчета duration и общие принципы использования в обоих калькуляторах абсолютно одинаковы. Наиболее подробно разбор принципов калькулирования представлен здесь, поэтому даже в случае использования второго варианта рекомендуется ознакомиться с этой инструкцией по стандартному калькулятору.
						h3.h3 Общие понятия
						h4.h4 1 час работы = порезка и стилизация 5 уникальных элементов.
						p При оценке учитываются все компоненты, на которые разработчик будет тратить время, в том числе и работа с неуникальным контентом (copy-paste).
						p Уникальным элементом является не повторяющаяся часть дизайна, на которую разработчику нужно потратить время для его порезки, стилизации, выравнивания и т.д. Например логотип, текстовый контент, кнопка, картинка, инпут формы, простой список, социалки, пагинация и т.д. Уникальный элемент считается только один раз в проекте, т.е. если один и тот же элемент повторяется на других страницах, то повторно он не выделяется и не влияет на duration.
						p Повторяющиеся блоки с измененным контентом считается как 1 элемент, т.е. если у нас есть например секция с постами, то мы считаем поэлементно только первый пост, a всё остальное уже copy paste (1 элемент). Если секция повторяется и контент в ней не меняется, на это времени добавлять не нужно, дополнительный элемент на copy-paste мы не ставим.
						p В duration, посчитанный согласно принципам данного подхода к оцениванию, входят не только порезка и стилизация элементов дизайна, но и время на:
						ul.estimation-list
							li.estimation-item первичный инвестигейт;
							li.estimation-item порезку иконок;
							li.estimation-item вдумчивую разработку и поиск оптимального решения;
							li.estimation-item самопроверку перед постановкой проекта на QA, т.е. проект должен быть проверен разработчиком на развалы, на соответствие дизайну, на соответствие спекам и фактически быть готовым к отправке заказчику;
						p Самым простым критерием проверки того, сделана ли самопроверка с надлежащим качеством, является отсутствие визуальных багов во всех поддерживаемых браузерах и тестовых девайсах, т.е. тех багов которые клиент может заметить невооруженным глазом в первые 5 минут просмотра проекта.
						h3.h3 Оценка JS опций
			transition(name="slide-fade-tutorial")
				.tutorial(
					v-show="isActiveTutorial"
					name="Tutorial"
					)
					button.close-btn(
						type="button"
						@click="closeTutorial"
						)
						span.i.i-cross
					.text-holder
						h2.h2 Разбор калькулятора
						h3.h3 Amount of Elements
						p Поле для ввода количества посчитанных элементов. 1 час работы = порезка и стилизация 5 уникальных элементов (12 мин. на 1 элемент). Это основное значение от которого будет рассчитываться количество часов на проект (duration).
						p В duration уже зашито 10% времени на инвестигейт, время на порезку иконок и на самопроверку, которую разработчик обязан делать перед постановкой на QA. Любой js который нужно будет прикрутить для реализации дизайнов, будь то Open close в футере, карусель из логотипов и т.п. считаются отдельно.
						h3.h3 Amount of Pages
						p Поле для ввода количества страниц. Это значение на расчет количества часов не влияет, оно нужно только для формирования summary для EM / PM.
						h3.h3 Layout Type
						p Fixed / Flexible layout - чистое / базовое время посчитанных элементов, т.е. сумма подсчитанных элементов умноженная на 12 минут.
						p Responsive at our discretion - к базовому времени на проект добавляется 50% (30% таблетка + 20% мобилка). Сюда входит бургер меню и непосредственно сам респонсив.
						ul.estimation-list.tutorial-list
							li.estimation-item + 1 Responsive Design - выбираем когда у клиента кроме дизайна для десктопа есть дополнительно респонсив дизайн (таблетка, мобилы, и т.д.). +2 +3 +4 Responsive Design выбираем в соответствии количеству доп. дизайнов. Сюда входит бургер меню и непосредственно сам респонсив.
							li.estimation-item + 1 Responsive Designs - +65%
							li.estimation-item + 2 Responsive Designs - +80%
							li.estimation-item + 3 Responsive Designs - +95%
							li.estimation-item + 4 Responsive Designs - +110%
						h3.h3 Additional Requirements
						p Есть два вида опций: фиксированные по часам и зависимые от объема проекта. В левой колонке находятся все фиксированные и в правой все зависимые.
						h3.h3 JS Options
						p Выбираем все js опции которые есть в проекте. Они на расчет количества часов не влияют, (никак не добавляют в сумму дюр), они нужны только для формирования summary для EM / PM, а ребята уже квотят клиента по стоимости опций. Кнопкой reset Js можно быстро сбросить выбранные строки.
						h3.h3 Extra Hours
						p Поле для ввода дополнительных часов. Если в проекте есть требования которых нет в калькуляторе, просто дописываем нужные часы на реализацию или риски, они будут учитываться в общем количестве часов на проект. Ниже в поле Notes / Questions описываем сколько и на что добавили.
						blockquote.estimation-blockquote
							h4.h4 Важно
							p Риски всегда должны выносится отдельно в поле Notes / Questions с пояснением. Нельзя закладывать риски в duration увеличивая количество элементов при разметке. Решение о включении или невключении рисков в стоимость и timeline проекта принимает PM.
						h3.h3 Notes / Questions
						p Поле для ввода описания к Extra Hours и дополнительных вопросов / комментариев.
						h3.h3 Days
						p Здесь отображается показатель timeline на проект без учёта времени на QA. На данный момент 2 значения: первое - из расчёта работы разработчика над проектом 7ч. в день, второе - из расчёта работы разработчика 6ч. в день, например когда у него помимо основного таска есть еще дополнительные задачи. По умолчанию из 8 рабочих часов мы рассчитываем на 7, т.к. 1 час уходит на стендапы, коммуникацию и т.д.
						h3.h3 Hours
						p Здесь отображается общее количество часов на проект.
						h3.h3 Summary
						p Здесь выводится общее summary по проекту. Кнопкой copy можно скопировать всё в буфер обмена для передачи инвестигейта EM / PM’у.
</template>

<script>
    export default {
        name: 'TheHeader',
        data () {
            return {
                isActive: false,
                isActiveTutorial: false
			}
		},
        methods: {
            crossEstimation(){
                this.isActive = !this.isActive;
                this.isActiveTutorial = false;
            },
            crossTutorial() {
                this.isActiveTutorial = !this.isActiveTutorial;
                this.isActive = false;
            },
            closeTutorial() {
                this.isActive = false;
                this.isActiveTutorial = false;
			}
        }
    }
</script>

<style lang="scss" scoped>
	@import '../scss/_base.scss';

	.header {
		min-height: 80px;
		border-bottom: 2px solid $bg-body;
		.container {
			position: relative;
			display: flex;
			justify-content: space-between;
			align-items: center;
			padding: 15px;
		}
	}

	.navbar {
		display: flex;
		flex-direction: column;
		padding-left: 0;
		@include media('>skyline-phone') {
			flex-direction: row;
		}
	}

	.navbar-item {
		margin-left: 15px;
		list-style-type: none;
		background: none;
		border: none;
		outline: none;
		transition: color .3s;
		display: flex;
		align-items: center;
		&:hover {
			color: $white;
		}
		&:nth-child(1) {
			margin-bottom: 10px;
			@include media('>skyline-phone') {
				margin-bottom: 0;
			}
		}
	}

	.i {
		padding-right: 5px;
	}

	.layer {
		position: absolute;
		width: 100vw;
		height: 100vh;
		opacity: 0;
	}

	.estimation,
	.tutorial {
		position: absolute;
		top: 80px;
		background: $white;
		border: 2px solid $color-input;
		left: 50%;
		transform: translateX(-50%);
		width: 80%;
		padding: 15px;
		z-index: 2;
		overflow-y: scroll;
		max-height: 80vh;
		@include media('>tablet') {
			padding: 40px;
		}
	}

	.slide-fade-enter-active,
	.slide-fade-leave-active {
		transition: all .7s ease;
	}

	.slide-fade-enter,
	.slide-fade-leave-to {
		transform: translate(-200%);
	}

	.slide-fade-tutorial-enter-active,
	.slide-fade-tutorial-leave-active {
		transition: all .7s ease;
	}

	.slide-fade-tutorial-enter,
	.slide-fade-tutorial-leave-to{
		transform: translate(-200%);
	}

</style>