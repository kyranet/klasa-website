<template>
	<footer class="footer">
		<div class="container">
			<div class="content has-text-centered">
				<p>
					<strong>Let's write clean code together!</strong>
				</p>
				<div class="columns">
					<div class="column is-two-fifths is-hidden-tablet" />
					<div class="column">
						<a href="https://www.npmjs.com/package/canvas-constructor" class="button is-danger">
							<span>Published using:</span>
							<span class="icon">
								<i class="fab fa-npm" />
							</span>
						</a>
					</div>
					<div class="column">
						<a href="https://www.patreon.com/kyranet" class="button is-patreon">
							<span>Support Kyra:</span>
							<span class="icon">
								<i class="fab fa-patreon" />
							</span>
						</a>
					</div>
					<div class="column">
						<a class="button is-dark" @click="toggleDark()">
							<span>{{ dark ? "Light" : "Dark" }} Mode</span>
							<span class="icon">
								<i :class="dark ? 'fas fa-sun' : 'fas fa-moon'" />
							</span>
						</a>
					</div>
					<div class="column is-two-fifths is-hidden-tablet" />
				</div>
				<stats />
			</div>
		</div>
	</footer>
</template>

<script>
import Stats from './Stats.vue';

export default {
	name: 'AppFooter',
	components: { Stats	},
	computed: {
		dark() {
			return this.$parent.dark;
		}
	},
	methods: {
		toggleDark() {
			this.$parent.dark = !this.$parent.dark;
			localStorage.setItem('dark', String(this.$parent.dark));
		}
	}
};
</script>
