# elixir-recipes

> Pull Requests are most welcome!

## Building

Create a new Markdown file in `source/_posts` with the right filename format. Examples can be found in the `source/_posts` directory.

```
jekyll serve
```

Go to `localhost:4000` to view the generated site.

## Contributing

The `source` branch contains the source Markdown posts in `/_posts`.
Create posts in Markdown and commit (on the `source` branch):

```
git add .
git commit 'Add new recipe'
git push
```

Then, send in a [pull request](https://github.com/Elixir-Recipes/elixir-recipes.github.io/pulls)!

## Deploying

```
rake publish
```

This command will build and push the local `_site` subdirectory to the `master` branch for Github Pages to render.

## Contributors

- [Yos Riady](https://github.com/Leventhan)
