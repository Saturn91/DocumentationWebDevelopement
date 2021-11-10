# Performance still matters in 2021

Lots of different devices have different performance abilities and different level internet connections

- Performance is Userexperience, Userexperience is money!
- Having better performance increases your position in Google searche lists
- every Website should load in 2s maximum! (after 3s most users will leave)
- Frameworks increased performance generally

# Why to optimize

- Optimisations should not be made for people who have bad internet in general, but for people who are sitting in the train and have temporarly week connection
- Also other countries might have bad internet!

# Why is it slow

## Images
- Most of the times images are to high resolution
- Use max. something like 1400px if the viewport is big
- Use max 300px on mobiles
- Use JPEG always for fotos!
  -  All devices seem to be able to display
  -  No transparancy (have to work arround)
- Progressive JPEGS -> allow a preloading with low res images and then post loading until the highest available image
- PNG 8 -> can be used for no transparent pictorgramms (because it optimzes images using vectores and therefore shapes)
- PNG 24 only when using transparency, slow!!
- WEBP: has lots of options safari has still its issue with it
- SVG's are really usefull if your graphic can be drew in vectors
- Intresting thought: there were Sprites (uploading a sprite atlas)
- Check out IMGIX.COM or KRAKEN.IO -> image processing and optimisation checkout API!

### Tipps
1. Is it a picture -> jpeg
2. Is it vectore based -> svg
3. Is it an animation -> gif
4. Use an image optimizer like kraken.io and imgix.com
5. https://images.guide
6. Analyse your websites files sizes (in dev mode network side)
7. use responsive images
8. develop for mobile first (you will never use a huge image!) > 80% of all users will access your website on mobile!!!

### Responsive images
```html
<!-- responsive images -->
<img srcset="elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 600px) 480px,
            800px"
     src="elva-fairy-800w.jpg"
     alt="Elva dressed as a fairy">
<!-- in this example the 480w refers to the whole viewport width-->
```

```html
<!-- use sizes to not use the whole viewport size but to refer to a supsize-->
<img srcset="large.jpg  1024w,
      medium.jpg 640w,
      small.jpg  320w"
   sizes="(min-width: 36em) 33.3vw,
      100vw"
   src="small.jpg"
   alt="A rad wolf" />

```

## CSS
1. use simple classes (header__button instead of header button)
2. optimize css split and make sure they get loaded when needed
3. (most modern frameworks are already optimized)
4. identify critical css and implement i.e. as inline css and then load rest later
5. Checkout: https://github.com/addyosmani/critical

## Load only what you need / Lazy loading
If you open a website on your mobile, even the huge invisible part of the website with your 20 images gets loaded even if the 20 images are not yet displayed. This can be optimized
We should load everything lazy, it is not always faisable. It is not aplicable in each browser... react and angular might handle it differently.
```html
<img src="image.jpg" alt="..." loading="lazy">
```

## Performance Budget
Give yourself a Target to achieve. I.e. I want to load the page within 1s. I want to have 15 FPS, < 5s in 3G

## Render Blocking / Blocking Javascript
- use defer or async tags when importing css

## Webfonts
- check Size just to be sure
- look into sub setting
- load font as defer or async
- checkout https://github.com/typekit

# Analyse your project
- https://www.webpagetest.org/

# Tipps
- repositioning (animations) should be done with transformations not top/left/down/right
- checkout CDN for further optimisation (server side rendering / caching)
- caching data which is not rerendered
- https://perf.rocks/
- gatsby.js framework
- if react than next.js
