# Templates

Templates repositories to use as base for repositories.

It also contains some other useful information irrelevant to templates.

## Content

- [Github steps](#github-steps)
- [TODO](#TODO)
- [Go template](go)
- [React Typescript template](react-ts)
- [NodeJS Typescript template](node-ts)
- [Useful sh commands and functions](sh.md)
- [Useful VSCode extensions](vscode.md)

## Github steps

1. [Create the repository on Github](https://github.com/new) picking the template you want.
1. [Turn on Travis CI](https://travis-ci.org/account/repositories) for that repository, and set the `DOCKER_PASSWORD` variable for all branches
1. Git clone the repository with:

    ```sh
    git clone git@github:qdm12/REPONAME_GITHUB.git
    cd REPONAME_GITHUB
    ```

1. Replace `REPONAME_GITHUB`, `REPONAME_DOCKER` and `SHORT_DESCRIPTION`:

    ```sh
    find ./ -type f -exec sed -i 's/REPONAME_DOCKER/realname/g' {} +
    find ./ -type f -exec sed -i 's/REPONAME_GITHUB/realname/g' {} +
    find ./ -type f -exec sed -i 's/SHORT_DESCRIPTION/realdescription/g' {} +
    ```

1. Work on the code and documentation, make sure:
    - Uou made a nice `title.svg` for the readme
    - Use `$(pwd)` for bind mounts with `docker run` commands
    - The container runs without root with `USER 1000` or `libcap` or `gosu`
    - Check the container can be restarted without permission issues
    - A healthcheck is implemented in the same program you are developing
1. Upload your changes

    ```sh
    git add . && git commit -m "Initial commit" && git push
    ```

1. Go to the Github repository [github.com/qdm12/REPONAME_GITHUB](https://github.com/qdm12/REPONAME_GITHUB) webpage
    1. Add topics
    1. Set the website to [hub.docker.com/r/qmcgaw/REPONAME_DOCKER](https://hub.docker.com/r/qmcgaw/REPONAME_DOCKER)
    1. Check [README.md](https://github.com/qdm12/REPONAME_GITHUB) formatting
1. Check the build status on Travis CI at [travis-ci.org/qdm12/REPONAME_GITHUB](https://travis-ci.org/qdm12/REPONAME_GITHUB)
1. Go to [microbadger.com/images/qmcgaw/REPONAME_DOCKER](https://microbadger.com/images/qmcgaw/REPONAME_DOCKER)
    1. Get the webhook link
    1. Replace the webhook link in `.travis.yml` with:

        ```sh
        sed -i 's/WEBHOOK_LINK/realwebhook/g' .travis.yml
        ```

1. Upload the changes

    ```sh
    git add . && git commit -m "Formatting fixes and microbadger link" && git push
    ```

## TODO

- Add github issues/PR templates
- Move from Travis to Github actions
