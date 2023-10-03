# Download romance novel cover thumbnail images

This project has been modified from The Pudding's [starter template](https://github.com/the-pudding/svelte-starter) to download and host images for a project on [romance novel covers](https://pudding.cool/2023/10/romance-covers/).

## Setup

#### Dependencies

- [node](https://nodejs.org/en/)
- [d3](https://d3js.org/)
- [fs](https://nodejs.org/api/fs.html)
- [image-downloader](https://lodash.com/](https://www.npmjs.com/package/image-downloader)

#### Install

Clone the repo and run `pnpm i`

## Reproduce

#### `npm run imgDownload`

Downloads all cover thumbnail images from the `cover_url` column in `src/data/listings.csv` and saves those files by their ISBN to `static/assets/images/img_${d.ISBN}.jpg`. Note: The photos are saved as-is and do not resize.


## Notes

Google Books does occasionally update their thumbnails so what they display (and what you download) today might not be a match for the images in this repo.
