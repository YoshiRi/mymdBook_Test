# mymdBook_Test
Test Project to use mdBook in GitHub Actions

## Set up

Minimal Setting will be like this.

```
mymdBook_Test
├── .github
│  └── workflow
│     └── mdBook.yml
│
├── book.toml
└── src
   ├── chapters
   │  ├── introduction.md
   │  └── <other .md files>
   └── SUMMARY.md
```

### mdBooks workflow


[.github/workflow/mdBook.yml](.github/workflow/mdBook.yml) configures CI build settings copied from [here](https://github.com/peaceiris/actions-mdbook).

Roughly speaking, it does something like:

1. Upload files to CI
2. Build mdbook
3. Push to gh-pages branch


```yml
name: github pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2

      - name: Setup mdBook
        uses: peaceiris/actions-mdbook@v1
        with:
          mdbook-version: '0.4.6'
          # mdbook-version: 'latest'

      - run: mdbook build

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./book
```

### book.toml

[book.toml](book.toml) is a configuration file.

### For further writings

See [official documentation](https://budziq.github.io/mdBook/cli/init.html).

## Compile and see locally

If you use docker in WSL(or Linux), just try following command.

```
wsl docker run --rm -v $(pwd):/book/ peaceiris/mdbook build
```

## Output

Finally you can see output page in [here](https://yoshiri.github.io/mymdBook_Test/).

