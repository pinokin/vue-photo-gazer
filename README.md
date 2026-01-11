# Photo Gazer

A simple image gallery using Vue in Vite.

<img alt="Status" title="Status" src="https://custom-icon-badges.demolab.com/badge/Status-Good%20enough-7C4F0B?style=for-the-badge&color=7C4F0B&labelColor=482C03" />

## Given requirements

- **Format.** The app needs to be a single-page application (SPA). -> Check, it's a basic Vue app.
- **Basic funtionality.** A grid view (a collection of images) and a details view (showing a single image and its data). -> Check, there's a list of images and you can click on them to see one at a time.

## My own constraints

- **Time.** I will work only a few hours (2-5 h) on this project. (_Yeah, well, 15 hours is still "a few", right...? I might have fallen into a few rabbit holes along the way._)
- **Accessibility.** The app needs to be navigable by keyboard and also make sense when using a screen reader.

## Nice to have features
Oh, time, there's never enough. Maybe I'll get to these in the future?

- **Pagination.** Now I'm only fetching the first 25 photos, pagination would be nice.
- **Styling.** My own styles without depending on Tailwind (or in this case on PicoCSS) or similar.
- **Animations and transitions.** Those would be cool.
- **Using IndexedDB.** Now I'm using localStorage, but if I were to flesh this app out, then using IndexedDB would make sense.

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
