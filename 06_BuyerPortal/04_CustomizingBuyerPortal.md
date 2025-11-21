# Customizing the Buyer Portal

## Step 1: Set Up Project

**Install yarn:**

```shell
npm i -g yarn
```

**Clone repo:**

```shell
git clone git@github.com:bigcommerce/b2b-buyer-portal.git
```

**Clone fork:**

```shell
git clone git@github.com:<YOUR_GITHUB_USERNAME>/<YOUR_FORK_NAME>.git
```

**Install dependencies:**

```shell
yarn install
```

**.env contents:**

```
VITE_LOCAL_DEBUG=TRUE
```

## Step 2: Configure B2B Store in Development

**Run dev server:**

```shell
yarn dev
```

## Deploying Your Custom Buyer Portal

**.env contents:**

```
VITE_ASSETS_ABSOLUTE_PATH='https://my.custom.cdn/b2b/assets/'
```

**Run build:**

```shell
yarn build:production
```
