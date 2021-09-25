# ic-staking-documentation

This is a GitHub page for creating documentation for easy user-facing staking within the Internet Computer. This is intended to be a community-driven set of documents.

You can see the GitHub page here: https://probable-goggles-3dc3d635.pages.github.io/

## How to contribute

The GitHub page is composed of pages in the `/docs` directory. Editing the copy is very easy.

## How to run this locally

To run this locally, you should follow the instructions at [Testing your GitHub Pages site locally with Jekyll](https://docs.GitHub.com/en/pages/setting-up-a-GitHub-pages-site-with-jekyll/testing-your-GitHub-pages-site-locally-with-jekyll).

## How to deploy changes

The GitHub page is tied to the branch `gh-pagess`. Anything that is merged to `gh-pages` branch automatically becomes deploys to the GitHub page.

## How to edit the styling

The current theme is the "Just the Docs" Jekyll theme.

* Documentation for "Just the Docs": https://pmarsceill.github.io/just-the-docs/
* GitHub page for "Just The Docs": https://github.com/pmarsceill/just-the-docs

If you want to change the theme altogether, you need to do the following: 

1. Edit the `_config.yml` file and edit the line that reads to add whatever theme you chose.

```
theme: "just-the-docs"
```

2. Run `gem install` to install the theme you chose
