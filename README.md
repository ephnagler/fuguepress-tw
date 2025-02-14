# Steps taken

1. shopify theme init 
    - name your theme / folder - we're using dawn
2. shopify theme dev
    - login to shopify, connect to your store
3. install tailwind (https://tailwindcss.com/docs/installation/tailwind-cli)[https://tailwindcss.com/docs/installation/tailwind-cli]
    - npm install tailwindcss @tailwindcss/cli
4. make an input css file in assets folder (labeled mine tw-input.css for easy ref)

inside input.css :

```
@import "tailwindcss";
```

5. add the script to your package.json file, change -i and -o paths to match assets folder and your tw css file and run tw to create your output file

```
{
  "scripts":{
    "tw" : "npx @tailwindcss/cli -i ./assets/tw-input.css -o ./assets/tw-output.css --watch",
    "dev": "shopify theme dev"
  },
```

6. lets run them together with concurrently
    - npm install concurrently --save-dev

7. add together on dev script, escaping quotations

```
  "scripts":{
    "tw" : "npx @tailwindcss/cli -i ./assets/tw-input.css -o ./assets/tw-output.css --watch",
    "dev": " concurrently \"shopify theme dev\" \"npx @tailwindcss/cli -i ./assets/tw-input.css -o ./assets/tw-output.css --watch\""
  },
```

8. then import the output css file  after the base.css in layout / theme.liquid

```
{{ 'tw-output.css' | asset_url | stylesheet_tag }}
```

9. clean up git and github

```
// disconnect from shopify's github
git remote remove origin

// clean up git history
rm -rf .git && git init

// initial git
git add .
git commit -m "Initial commit - <your theme>"

```

10. add DaisyUI

```
  npm i -D daisyui@latest 
  
  // or in my case: 
  npm i -D daisyui@beta
```

11. add DaisyUI as a Tailwind plugin in your tw-input.css

```
@import "tailwindcss";
@plugin "daisyui";
```

12. install theme-change

(https://github.com/saadeghi/theme-change)[https://github.com/saadeghi/theme-change]