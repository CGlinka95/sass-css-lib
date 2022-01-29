# Sprout

## sass-css-lib Notes & Explanations

### My first css library to practice sass and other node packages, such as gulp

- Sass compiled using gulp and js functionality in gulpfile.js:

Required gulp imports for sass functionality:

```bash
    const {src, dest, watch, series} = require('gulp')
    const sass = require('gulp-sass')(require ('sass'))
```

buildStyles function that updates index.css with browser valid css, compiled from index.scss:

```bash
    function buildStyles() {
        return src('scss/**/*.scss')
            .pipe(sass())
            .pipe(dest('css'))
    }
```

watchTask function that watches the index.scss file for valid sass changes, then calls the buildStyles function to update index.css.

```bash
    function watchTask() {
        watch(['scss/**/*.scss'], buildStyles)
    }
```

- The purpose here is to keep both files in sync with one another.

- *.scss = search for any named file with the .scss file extension.

- **/*.scss = search through sub folders inside parent directory.

Finally, I export by default the series variable, calling both functions:

```bash
    exports.default = series(buildStyles, watchTask)
```

## Variables

- Variables are created using the syntax $variableName: property;

- Varaiables may then be called with the $variableName when allocating that property to an element.

- The purpose of variables is to modularize your css, thus, making it easier to work with in the future.

## Partials

- A partial is a separate .scss file that houses modularized code, such as variables. Eg. variables.scss. Preventing your index.scss from getting bogged down with unecessary additional lines of code.

- Next, we must import our partial into our main index.scss file, so that the code is still accessable.

```bash
    @import 'variables';
```

- The issue with this, however, is that when our compiler (gulp in this case) compiles our sass into valid css, it will compile other named .scss files as well, creating unecessary blank .css files.

- The way we get around this issue is by adding an '_' in front of any .scss files that we want the compiler to ignore:_variables.scss
