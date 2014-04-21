# flynn-cli-dist

A suite of tools for building [flynn-cli](https://gitub.com/flynn/flynn-cli),
generating binary diffs, and distributing them for updates.

## Prerequisites

install [godep](https://github.com/kr/godep) to manage dependencies:

```bash
$ go get github.com/kr/godep
```

## environment

### DISTURL (build)

url for the flynn-cli directory server (e.g. https://flynn-cli.herokuapp.com)

### S3DISTURL (build, gen, web)

url for the S3 bucket for distributing full flynn-cli binaries (e.g. https://flynn-cli-dist.s3.amazonaws.com/)

### S3PATCHURL (gen)

url for the S3 bucket for distributing patches
(e.g. https://flynn-cli-patch.s3.amazonaws.com/)

### S3_ACCESS_KEY (build, gen), S3_SECRET_KEY (build, gen)

aws iam credentials

### BUILDNAME (build)

the name of the binary to build (e.g. "flynn")

### BUILDBRANCH (build)

the name of the git branch to build from (e.g. "master")

### DATABASE_URL (web)

postgres:// url

### PORT (web)

which tcp port to listen on

### HKGENAPPNAME (build)

the name of the heroku app to generate diffs with

## Creating a new release

To release a new version of flynn-cli:

1. make a gpg-signed git tag of the form vYYYYMMDD or vYYYYMMDD.N

    ```bash
    $ git tag -sam "added a new feature" vYYYYMMDD
    ```

2. push the release branch to that tag on github

    ```bash
    $ git co release
    $ git reset --hard vYYYYMMDD
    $ git push origin release
    ```

3. run flynn-cli-dist build to build for all platforms and generate diffs

    ```bash
    ## Export environment variables for target build ##
    $ flynn-cli-dist build
      ...
    ```


## Credits

This is a fork of Heroku's [hkdist](https://github.com/heroku/hk/tree/master/hkdist).
