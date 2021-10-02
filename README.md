# IC staking with self-custody

This is a GitHub page for creating documentation for easy self-custody staking within the Internet Computer. This is intended to be a community-driven set of documents.

You can see the GitHub page here: https://dfinity.github.io/ic-staking-documentation/

(@dprats note: the code is deployed as a github page solely to maximize public/community development + deploy. This could easily be a canister smart contract as well. That will be a good next iteration and I am working on deploying it to IC)

* * *
## Relevant background and reading

### Staking and NNS
* [The Network Nervous System: Governing the Internet Computer](https://medium.com/dfinity/the-network-nervous-system-governing-the-internet-computer-1d176605d66a)
* [The Community-Led Governance of the Internet Computer](https://medium.com/dfinity/the-community-led-governance-of-the-internet-computer-b863cd2975ba)
* [Earn Substantial Voting Rewards by Staking in the Network Nervous System](https://medium.com/dfinity/earn-substantial-voting-rewards-by-staking-in-the-network-nervous-system-7eb5cf988182)
* [The Internet Computer’s NNS Front-End Dapp Is Now Open Source](https://medium.com/dfinity/the-internet-computers-nns-front-end-dapp-is-now-open-source-3925edc21c49)
* [How to Deploy Your First Canister Smart Contract Using the NNS Dapp](https://medium.com/dfinity/how-to-deploy-your-first-canister-using-the-nns-dapp-c8b75e01a05b)
* [Get Started Using the NNS Front-End Dapp and ICP Wallet on the Internet Computer](https://medium.com/dfinity/getting-started-on-the-internet-computers-network-nervous-system-app-wallet-61ecf111ea11)

### Internet Computer
* [How the Internet Computer works](https://dfinity.org/howitworks/)
* [Showcase of apps on the Internet Computer](https://dfinity.org/showcase)
* [Coding on the Internet Computer](https://smartcontracts.org/)
* [Internet Computer replica code](https://github.com/dfinity/ic)
* [Motoko Playground](https://m7sm4-2iaaa-aaaab-qabra-cai.raw.ic0.app/)
* [Developer Forum](https://forum.dfinity.org/)

* * *
## How to contribute

The GitHub page is composed of pages in the `/docs` directory. Editing the copy is just markdown.

* * *
## How to run this locally

To run this locally, you should follow the instructions at .

1. Pull down repo
2. Setup Jekyll and other Gems necessary as denoted here [Testing your GitHub Pages site locally with Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)
3. Navigate to /docs
4. Run 
```bash 
$ bundle exec jekyll serve
``` 

* * *
## How to deploy changes

The GitHub page is tied to the branch `main`. Anything that is merged to `main` branch automatically becomes deploys to the GitHub page: https://dfinity.github.io/ic-staking-documentation/

* * *
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
