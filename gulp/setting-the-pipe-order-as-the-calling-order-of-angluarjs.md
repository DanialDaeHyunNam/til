## When combining all the JS files should set the pipe order as the calling order of AngularJS 1.X functions

```javascript
gulp.task("js-combine", () => {
  return gulp.src([
            pkg.paths.build.js + "app/*.min.js",
            pkg.paths.build.js + "controllers/*.min.js",
            pkg.paths.build.js + "services/*.min.js",
            pkg.paths.build.js + "factories/*.min.js"
       ])
       .pipe($.plumber({errorHandler: onError}))
       .pipe($.newer({dest: pkg.paths.dist.js + pkg.vars.siteJsName}))
       .pipe($.concat(pkg.vars.siteJsName))
       .pipe($.size({gzip: true, showFiles: true}))
       .pipe(gulp.dest(pkg.paths.dist.js))
       .pipe($.filter("**/*.js"))
       .pipe($.livereload());
});
```

## Reference
[What is the calling order of angularjs functions (config/run/controller)?](https://stackoverflow.com/questions/38374145/what-is-the-calling-order-of-angularjs-functions-config-run-controller)
