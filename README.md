# sveltekit-tasks
A basic tasks app created with sveltekit and svelte 5 features like runes, snippets etc.

# Bulma integration
For styling Bulma v1 is integrated in this project

## Install
`npm i -D sass svelte-preprocess bulma`

## svelte.config.js
```
import adapter from '@sveltejs/adapter-auto'
import preprocess from 'svelte-preprocess'


// eslint-disable-next-line no-unused-vars
/** @type {import('@sveltejs/kit').Config} */
const config = {
	preprocess: preprocess({
		scss: {
			prependData: "@import './src/app.scss';",
		}
	}),
    // Remove vite-plugin-svelte warnings about unused CSS selectors
    onwarn: (warning, handler) => {
        const { code, frame } = warning;
        if (code === 'css-unused-selector') return;
        handler(warning);
    },
	kit: {
		adapter: adapter()
	}
};

export default config;
```
## Root +layout.svelte
```
<script>
    import '../app.scss'
    let { children } = $props() 
</script>

{@render children()}
```

## app.scss
```
@import "bulma"
```
