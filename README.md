# Gulp for XAMPP

This project is a [Gulp.js](https://gulpjs.com/) configuration for developing WordPress themes on top of [XAMPP](https://www.apachefriends.org/download.html). It implements SASS, CSS and Javascript minification and (optional) combination, and image optimization, as well as [BrowserSync](https://browsersync.io/) to streamline development.

## Setup

This project requires [Node.js](https://nodejs.org/en). Once you have Node.js installed, you'll need to install the Gulp command line interface:

```bash
npm install -g gulp-cli
```

Then enter the directory for your WordPress theme and run the following commands (assuming your folder does not already contain a Node.js project):

```bash
npm init
npm install --save-dev autoprefixer browser-sync cssnano gulp-concat gulp-deporder gulp-imagemin gulp-newer gulp-postcss gulp-sass gulp-strip-debug gulp-uglify postcss-assets
```

Next, copy **gulpfile.js** from this repository into the theme directory.

## File Structure

This configuration file assumes your WordPress theme has a directory structure similar to this:

```text
/your_theme/
├── /css/
│   └── another_style.css
├── /img/
│   ├── img1.jpg
│   └── img2.png
├── /inc/
├── /js/
│   ├── script1.js
│   └── script2.js
├── /src/
│   ├── /img/
│   │   ├── img1.jpg
│   │   └── img2.png
│   ├── /js/
│   │   ├── script1.js
│   │   └── script2.js
│   └── /scss/
│       ├── another_style.scss
│       └── style.scss
├── /template-parts
├── .gitignore
├── 404.php
├── archive.php
├── footer.php
├── functions.php
├── gulpfile.js
├── header.php
├── index.php
├── page.php
├── search.php
├── single.php
└── style.css
```

You'll author SASS and Javascript files, and put your images, in their respective directories within the **/src/** folder. The file **/src/scss/style.scss** will be compiled and exported as your default WordPress stylesheet at **/style.css**. Other SASS and CSS files in **/src/scss/** directory will be compiled and piped to **/css**. Javascript files in **/src/js** will be minified and (optionally) combined, then exported to **/js**. Finally, images in **/src/img/** will be optimized and exported to **/img**.

## Configuration

The only variables you definitely need to configure are:

1. **wordpress_project_name**: this is the name of your project; it should be the name of the folder within the XAMPP **htdocs** folder where your WordPress installation lives.
2. **theme_name**: the name of your theme; it should match the theme folder name. So you should be able to find the theme folder at: htdocs/**wordpress_project_name**/wp-content/themes/**theme_name**/

If you've changed the default settings for XAMPP, so that your development site is accessed from any URL other than localhost/**wordpress_project_name**, you will also need to reconfigure the **browserSyncProxy** variable.

By default, Javascript files are not combined. If you want to combine your Javascript files, uncomment the line reading ".pipe(concat(js.filename))" in the **processJS** method. By default, scripts will be combined into **/js/scripts.js**; you can change that behavior by changing the **filename** variable within the **js** options object.

## Running the Development Environment

Start XAMPP via the XAMPP control panel. Then open your terminal in the theme directory and run:

```bash
gulp develop
```

Your BrowserSync proxy (where you should access the development site) will be available at **localhost:3000/your_site/**. The BrowserSync UI will be available at **localhost:8001**.
