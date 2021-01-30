# mymdBook_Test
Test Project to use mdBook in GitHub Actions

## Set up

Minimal Setting will be like this.

```
mymdBook_Test
├── .github
│  └── workflow
│     └── mdBook.yml
└── src
   ├── chapters
   │  ├── introduction.md
   │  └── <other .md files>
   └── SUMMARY.md
```

### mdBooks workflow

Sample yml file is [here](https://github.com/peaceiris/actions-mdbook).

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



## How to

Finally you can see output page in [here](https://yoshiri.github.io/mymdBook_Test/).

