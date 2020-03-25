# Templates

Templates repositories to use as base for repositories.
These are shown above as Git submodules and can be accessed by clicking on them.

It also contains some other useful information irrelevant to templates.

## Content

- [Github steps](#github-steps)
- [Other](#other)
- [TODO](#TODO)

## Github steps

1. [Create the repository on Github](https://github.com/new) picking the template you want.
1. Set secrets in [https://github.com/qdm12/REPONAME_GITHUB/settings/secrets](https://github.com/qdm12/REPONAME_GITHUB/settings/secrets)
    - `DOCKERHUB_PASSWORD`
    - `PHONITO_TOKEN` (if final Docker image is not based on Scratch)
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
    - Use `$(pwd)` for bind mounts with `docker run` commands
    - The container runs without root with `USER 1000` or `libcap` or `gosu`
    - Check the container can be restarted without permission issues
    - A healthcheck endpoint and Docker is implemented if possible
1. Upload your changes

    ```sh
    git add . && git commit -m "Initial commit" && git push
    ```

1. Go to the Github repository [github.com/qdm12/REPONAME_GITHUB](https://github.com/qdm12/REPONAME_GITHUB) webpage
    1. Add topics
    1. Set the website to [hub.docker.com/r/qmcgaw/REPONAME_DOCKER](https://hub.docker.com/r/qmcgaw/REPONAME_DOCKER)
    1. Check [README.md](https://github.com/qdm12/REPONAME_GITHUB) formatting
    1. Set the social preview at [https://github.com/qdm12/REPONAME_GITHUB/settings](https://github.com/qdm12/REPONAME_GITHUB/settings)
1. Check the workflows at [https://github.com/qdm12/REPONAME_GITHUB/actions](https://github.com/qdm12/REPONAME_GITHUB/actions)
1. Go to [microbadger.com/images/qmcgaw/REPONAME_DOCKER](https://microbadger.com/images/qmcgaw/REPONAME_DOCKER)
    1. Get the webhook link
    1. Replace the webhook link in `.github/workflows/build-*.yml` with:

        ```sh
        sed -i 's/WEBHOOK_LINK/realwebhook/g' .github/workflows/build-*.yml
        ```

1. Upload the changes

    ```sh
    git add . && git commit -m "Formatting fixes and microbadger link" && git push
    ```

## Other

- [Useful sh commands and functions](sh.md)
- [Useful VSCode extensions](vscode.md)

## TODO

- Add github issues/PR templates
- Other github special files
- React components libary template using [Storybook](https://storybook.js.org/)
