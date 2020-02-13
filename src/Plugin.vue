<template>
	<div>
		<div class="uk-flex uk-flex-start">
			<div>
				Current version:
				<b>{{ model.version }}</b>
			</div>
		</div>
	</div>
</template>

<script>
import { PLUGIN_NAME } from './const';

export default {
	mixins: [window.Storyblok.plugin],
	data() {
		return {};
	},
	methods: {
		getDefaults() {
			return {
				plugin: PLUGIN_NAME,
				version: ''
			};
		},
		getComputed() {
			// console.log('sbe-component-version', 'plugin:computed', this.options);
			// defaults
			const defaults = this.getDefaults();

			// constraints checks are left to the browser
			const computed = {
				...defaults,
				version: this.options.version
			};

			// return the computed
			return computed;
		},
		initWith() {
			// console.log('sbe-component-version', 'plugin:init', this.options);
			// if options are initialized
			if (this.options) return this.getComputed();

			// otherwise the defaults
			return this.getDefaults();
		},
		pluginCreated() {
			// console.log('sbe-component-version', 'plugin:created', this.options);
		}
	},
	watch: {
		model: {
			handler(value) {
				this.$emit('changed-model', value);
			},
			deep: true
		}
	}
};
</script>

<style></style>
