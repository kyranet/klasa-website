<template>
	<nav class="columns is-mobile">
		<div class="column has-text-centered">
			<div>
				<p class="heading">
					Downloads
				</p>
				<p class="title is-size-5">
					{{ downloads }}
				</p>
			</div>
		</div>
		<div class="column has-text-centered">
			<div>
				<p class="heading">
					Stars
				</p>
				<p class="title is-size-5">
					{{ stars }}
				</p>
			</div>
		</div>
		<div class="column has-text-centered">
			<div>
				<p class="heading">
					Contributors
				</p>
				<p class="title is-size-5">
					{{ contributors }}
				</p>
			</div>
		</div>
	</nav>
</template>

<script>
const noop = () => {
	// noop
};
const json = res => res.json();

export default {
	name: 'Stats',
	data() {
		return {
			downloads: '27000+',
			stars: '30+',
			contributors: '10+',
			fetching: false
		};
	},
	beforeMount() {
		this.fetch();
	},
	methods: {
		async fetch() {
			if (this.fetching) return;
			this.fetching = true;

			const [downloads, stars, contributors] = await Promise.all([
				fetch('https://api.npmjs.org/downloads/range/2013-08-21:2100-08-21/canvas-constructor').then(json).catch(noop),
				fetch('https://api.github.com/repos/kyranet/canvasConstructor').then(json).catch(noop),
				fetch('https://api.github.com/repos/kyranet/canvasConstructor/stats/contributors').then(json).catch(noop)
			]);

			if (downloads) {
				this.downloads = 0;
				for (const item of downloads.downloads) this.downloads += item.downloads;
				this.downloads = this.downloads.toLocaleString();
			}
			if (stars) this.stars = stars.stargazers_count.toLocaleString();
			if (contributors) this.contributors = contributors.length.toLocaleString();
		}
	}
};
</script>
