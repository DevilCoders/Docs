Setup
=====

Project is built using `Next.js` React framework, based on a Yandex project template
for outsource developers (see upper-level README).

Install and Run
---------------

To install:
* Install packages as described in upper-level README
* Duplicate `.env.example` and rename copy to `.env`

To lint and launch:
* See upper-level README

To build ready for deploy node.js version:
* `npm run build` (note that language selection in this case will be performed dynamically on server-side based on host name and values of ENV variables described below)

.env Configuration  
------------------

`.env` file contains the following config variables:
* `REACT_APP_HOST_RU` - Host name of the Russian version site, w/o `http://` (used to load proper language)
* `REACT_APP_HOST_EN` - Host name of the English version site, w/o `http://` (used to load proper language)
* `REACT_APP_STAGING` - boolean flag indicating staging environment (`true` or `false`);
used for setting up proper `robots.txt` version for staging vs. production (disallow indexing on staging,
allow on production; disable Yandex.Metrika counter on staging, enable on production)
* `REACT_APP_PREFIX` - prefix used for url of the pages; e.g. when set to `/championship` Frontend page will be
available on the `/championship/frontend` url, rather than just `/frontend` (implemented for the links only,
no `/static` directory path mapping are implemented)
* `REACT_APP_ASSETS_PREFIX` - prefix used for url of the assets (js, css, content of `assets` folder,
e.g. when serving them from CDN), see [docs](https://nextjs.org/docs/api-reference/next.config.js/cdn-support-with-asset-prefix) for details
* `REACT_APP_STATIC_PREFIX` - prefix used for url of the static files usually served from `/public` directory
(images, etc., e.g. when serving them from CDN)

The exact same variables should be provided in your hosting environment (staging and production),
e.g. Config Vars on Heroku.

Compile for Production
----------------------

Run `npm run build`, optimized and ready for production version of an application will be created inside `.next` directory
(requires a Node.js environment to run).

Run `npm run start` to launch Node.js server for built version.

Content
=======

Content is generally managed through `.json` files.

Text and Block Contents
-------------

Text content is stored in `ru/*.json` and `en/*.json` files in `/content` directory (static content, baked in when building) and/or `/bunker` directory (mock files of the content, that will be served through Bunker in production). General content of the pages is stored in files with names starting with `page*`,
e.g. `pageHome.json` or `page_index.json` may contain text for the Home page, etc.

JSON files in `/bunker` directory should be accompanied with corresponding `*.schema.json` files (with JSON Schema for the content, that will be used in Bunker).

Content of the specific blocks and sections of the site may be stored in corresponding files as well. E.g., content
for Teachers Photo Gallery can be stored separately in `photoGalleryTeachers.json` and contain path to images within `/public/static/images`
directory (see below) and image descriptions.

Most of content supports Markdown syntax.

SEO
---

`.json` files of the pages contain `"seo"` group with the keys `"title"`, `"description"`, `"keywords"` for adding
corresponding meta data (and `og:` tags) to the page.

`default.json` contains default meta data for the pages as well as name of the thumbnail image (which may be
displayed when sharing a link on social media). Provided thumbnail is called `social-share.png` and is stored
in `/public/static` directory. It also contains Yandex.Metrika counter ID.

Block Visibility
-----------------

It is possible to turn on and off some of the blocks on pages by editing settings in the
`.json` file of the corresponding page (if present). E.g., to turn on Teachers Photo Gallery on Home page set
`"showTeachersPhotoSection"` key to `true`.

Settings
-----------------

Additional global settings may be stored in `settings.json`, e.g. settings for enabling/disabling some functionality based on boolean flags (e.g., `testEnded`, `supportEnded`, etc. keys).

Images
------

Images are stored in `/public/static/images` directory.


