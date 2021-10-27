# tailwindcss-bug

Removing `shadow-md` from ./components/button.css allows `npm run prod` to compile tailwindcss succesfully, otherwise we get:

```bash
➜  tailwind npm run prod

> @alphateknova/tailwindcss@1.0.0 prod
> NODE_ENV=production postcss tailwind-source.css -o tailwind-styles.css


warn - You have enabled the JIT engine which is currently in preview.
warn - Preview features are not covered by semver, may introduce breaking changes, and can change at any time.
TypeError: Cannot read property 'filter' of undefined
    at /home/ant/dev/tailwind/node_modules/tailwindcss/lib/jit/lib/resolveDefaultsAtRules.js:39:60
    at Array.map (<anonymous>)
    at Root.map (/home/ant/dev/tailwind/node_modules/postcss-selector-parser/dist/selectors/container.js:347:23)
    at Processor.func (/home/ant/dev/tailwind/node_modules/tailwindcss/lib/jit/lib/resolveDefaultsAtRules.js:38:20)
    at Processor._runSync (/home/ant/dev/tailwind/node_modules/postcss-selector-parser/dist/processor.js:102:26)
    at Processor.transformSync (/home/ant/dev/tailwind/node_modules/postcss-selector-parser/dist/processor.js:171:17)
    at extractElementSelector (/home/ant/dev/tailwind/node_modules/tailwindcss/lib/jit/lib/resolveDefaultsAtRules.js:47:47)
    at /home/ant/dev/tailwind/node_modules/tailwindcss/lib/jit/lib/resolveDefaultsAtRules.js:82:30
    at /home/ant/dev/tailwind/node_modules/tailwindcss/lib/jit/processTailwindFeatures.js:64:50
    at /home/ant/dev/tailwind/node_modules/tailwindcss/lib/jit/index.js:25:56
```

I found another class that causes the above error:

Adding the following to .btn in button.css throws that TypeError as well:

```css
@layer components {
    .btn {
        &:active {
             @apply ring ring-secondary ring-offset-2
        }
    }
}

```