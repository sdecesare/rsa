The browser bundle in dist/vendor/formatter.js is reused from Publication Studio. This source wrapper imports citeproc 2.4.63, @citation-js/core 0.7.21, and @citation-js/plugin-bibtex 0.7.21. It was bundled as ESM using esbuild 0.25.x. Citation style and locale XML files are shipped alongside the bundle with their original attribution.

To rebuild this optional vendor asset in a separate temporary checkout:

npm install citeproc@2.4.63 @citation-js/core@0.7.21 @citation-js/plugin-bibtex@0.7.21 esbuild@0.25
npx esbuild source/formatter.js --bundle --format=esm --minify --outfile=dist/vendor/formatter.js

The applicant app otherwise needs no package installation or build step.
