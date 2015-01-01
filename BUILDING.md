# Contribute to [jqnpm](https://github.com/joelpurra/jqnpm)

This is experimental software, so [feedback is most appreciated](https://github.com/joelpurra/jqnpm/blob/master/CONTRIBUTE.md)!



## Additional development requirements

- [shUnit2](https://shunit2.googlecode.com/) 2.1.x+ in your `$PATH`.



## Steps

1. Run `git clean -idX :/` to clean up any generated file. Use with care.
1. Create a new `git branch` where you add your changes.
1. Edit `src/jqnpm` with your changes
  - Follow current conventions to increase the chance of your patch being accepted.
1. Write additional tests in a subfolder to `tests/`.
  - Code with tests have a much, much higher chance of being accepted.
1. If you have changed code in `tests/*/package-source` subfolders, run `./tests/create-bundles.sh` to regenerate git `.bundle` files for tests.
1. Run tests with `./tests/all.sh`.
1. Repeat until your feature is done, well tested and all tests pass.
1. Create a pull request based on your new branch.


## Override for the *temporary `jq` wrapper* `jqnpm execute`

If you are runnings tests agains plain `jq`, it used to be a hassle to replace `jqnpm execute`. Now it's easy.

```bash
cd tests/
echo 'jq "$@"' >"jq-command-override.sh"
chmod u+x "jq-command-override.sh"
```

Now you can run `./tests/all.sh` against `jq` instead of using the *temporary `jq` wrapper* `jqnpm execute` - it is not to be used once `jq` is up to speed.



## Larger `jq.json` example.

This example shows the work-in-progress goal for `jq.json` metadata. It *can* be used in a centralized service, although none is devloped yet.


```json
{
    "name": "jq-one-single-utility",
    "version": "0.1.0",
    "description": "My awesome jq utility",
    "homepage": "https://github.com/joelpurra/jq-one-single-utility",
    "bugs": "https://github.com/joelpurra/jq-one-single-utility/issues",
    "author": {
        "name": "Joel Purra",
        "url": "http://joelpurra.com/"
    },
    "main": "./src/jq-one-single-utility.jq",
    "repository": {
        "type": "git",
        "url": "git://github.com/joelpurra/jq-one-single-utility.git"
    },
    "dependencies": {
        "joelpurra/jq-another-utility": "^1.0.0",
        "anotheruser/jq-url-splitting": "^2.3.4",
        "someuser/jq-smart-object-merging": "^0.7.1",
    },
    "engines": {
        "jq": "^1.5.0",
        "jqnpm": "^1.0.0"
    },
    "licenses": [{
        "type": "MIT",
        "url": "http://joelpurra.mit-license.org/2014"
    }],
    "keywords": [
        "jq-package"
    ]
}
```