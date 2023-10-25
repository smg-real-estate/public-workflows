# Collection of GitHub workflows

### poetry.yml

A [Poetry](https://python-poetry.org/)-based workflow that runs jobs in a custom Docker image.
This workflow provides a job `scripts`, that checks out a project, installs its dependencies
and optionally runs list of scripts, provided in `poetry_scripts` input using `poetry run`
command in a Python environment with all project dependencies.

It can be conveniently complemented by [Poe the Poet](https://github.com/nat-n/poethepoet)
scripts.

It has the following inputs to control its behaviour:
- `image_name` - Docker image for the job container
- `image_options` -  Options to pass to Docker
- `poetry_scripts` - List of scripts to run, e.G. `'["poe lint-all", "poe test-unit"]'`
- `debug` - Use this boolean input to troubleshoot poetry dependencies installation with richer log output
- `home` - Allows to override the value of $HOME environment variable, which is set by GitHub when running
    jobs in a custom Docker image

If you specify `image_name`, don't forget to provide `DOCKER_USERNAME` and `DOCKER_PASSWORD` secrets.

In addition, if you provide `SSH_KEY` secret, it will be added as a private SSH key to the home folder.
You can use this to install dependencies from private GitHub repositories or other private servers.
