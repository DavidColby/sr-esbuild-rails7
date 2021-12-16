Until StimulusReflex has an installer that works with non-webpacker setups, don't follow the setup guide all the way through.

Instead start here:

```
bundle add stimulus_reflex --version 3.5.0.pre8
yarn add stimulus_reflex@3.5.0.pre8
rails dev:cache
rails generate stimulus_reflex:initializer
```

Note that these are lifted from the [setup guide](https://docs.stimulusreflex.com/v/v3.5/hello-world/setup), with the extremely important removals of `rake webpacker:install:stimulus` and `rake stimulus_reflex:install`. Those commands won't work without webpacker, and may make things harder for you by creating incorrect configurations on the way.

After those tasks from your terminal, next replace the `@hotwired/stimulus` yarn package with `stimulus` in your package.json:

```json
{
  "name": "app",
  "private": "true",
  "dependencies": {
    "stimulus": "^3.0.1",
    "@hotwired/turbo-rails": "^7.1.0",
    "esbuild": "^0.14.5",
    "stimulus_reflex": "^3.5.0-pre8"
  },
  "scripts": {
    "build": "esbuild app/javascript/*.* --bundle --sourcemap --outdir=app/assets/builds"
  }
}
```

Then, manually create the application controller for SR:

```
touch app/javascript/controllers/application_controller.js
```

Fill that in with the contents found [here](https://github.com/DavidColby/sr-esbuild-rails7/blob/main/app/javascript/controllers/application_controller.js)

Then update `app/javascript/controllers/application.js` with the contents found [here](https://github.com/DavidColby/sr-esbuild-rails7/blob/main/app/javascript/controllers/application.js)

After that, you can jump back over to following along with the setup guide's manual-configuration section, starting with caching updates.

You can see the full set of changes to get SR working in [this commit](https://github.com/DavidColby/sr-esbuild-rails7/commit/c2541185407f558d8c0be2f3fc15de64a37a4de8), which picks up after the bundle and yarn add commands.
