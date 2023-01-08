## Notes

This has been designed mobile first and is responsive for 2 breakpoints. I did not receive any assets so I have put placeholders as backup. I would lazyload these images using something like https://www.npmjs.com/package/vue-lazyload if there were 100s of images. 

I originally hid the scrollbars with div::-webkit-scrollbar {
  display: none; /* for Chrome, Safari, and Opera */
}
but it felt a bit obscure to the user so I left it out.

I did not write unit tests as most of this was cosmetic and I feel like I would be testing Vue functionality rather than code functionality. 

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

