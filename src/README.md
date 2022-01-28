# sass-css-lib Notes & Explanations

## My first css library to practice sass and other node packages, such as gulp

- Sass compiled using gulp and js functionality in gulpfile.js:

Required gulp imports for sass functionality:

```bash
    const {src, dest, watch, series} = require('gulp')
    const sass = require('gulp-sass')(require ('sass'))
```

buildStyles function that updates index.css with browser valid css, compiled from index.scss:

```bash
    function buildStyles() {
        return src('index.scss')
            .pipe(sass())
            .pipe(dest('css'))
    }
```

watchTask function that watches the index.scss file for valid sass changes, then calls the buildStyles function to update index.css.

```bash
    function watchTask() {
        watch(['index.scss'], buildStyles)
    }
```

- The purpose here is to keep both files in sync with one another.

Finally, I export by default the series variable, calling both functions:

```bash
    exports.default = series(buildStyles, watchTask)
```
