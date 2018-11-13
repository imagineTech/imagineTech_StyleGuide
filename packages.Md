# Packages

As we grow, we will run into many different forms of packages and some of them will so efficient that we migrate them into our general project development. This file will list out our preferred configurartion and preferrences for these packages. 

Included:
 - Prettier

## Prettier Configuration

To make sure we also upkeep a consistent, best practice code style, we will be working with Prettier and with the use of CRA (Create-React-App), we can place the following configuration for prettier within our `package.json` file:

```
  "eslintConfig": {
    "extends": "react-app",
    "plugins": [
      "prettier"
    ],
    "rules": {
      "prettier/prettier": "error"
    },
    "husky": {
      "hooks": {
        "pre-commit": "pretty-quick --staged"
      }
    }
  }
```

Please note that we are using `devDependencies` such as `eslint-plugin-prettier`, `husky`, and `pretty-quick`. Also any additional prettier configuration should be done in a `.prettierrc.json` file.
