# Collection of GitHub workflows

### poetry.yml workflow

A [Poetry](https://python-poetry.org/)-based workflow that runs jobs in a custom Docker image.
This workflow provides a job `scripts`, that checks out a project, installs its dependencies
and optionally runs list of scripts, provided in `poetry_scripts` input using `poetry run`
command in a Python environment with all project dependencies.

It can be conveniently complemented by [Poe the Poet](https://github.com/nat-n/poethepoet)
scripts.

It has the following inputs to control its behaviour:

- `image_name` - Docker image for the job container
- `image_options` - Options to pass to Docker (optional)
- `pre-install` - Command to run before installing dependencies (optional)
- `poetry_scripts` - List of scripts to run, e.G. `'["poe lint-all", "poe test-unit"]'` (optional)
- `pip-constraint` - Path to pip constraint file that is used to install dependencies (optional)
- `debug` - Use this boolean input to troubleshoot poetry dependencies installation with richer log output (optional)
- `home` - Allows to override the value of $HOME environment variable, which is set by GitHub when running (optional)
  jobs in a custom Docker image
- `github_app_id` (and `github_app_private_key` secret) to provide GitHub app credentials used to
  generate GitHub token that will be used to access GitHub for `git+https://` dependencies (optional)

If you specify `image_name`, don't forget to provide `DOCKER_USERNAME` and `DOCKER_PASSWORD` secrets.

In addition, if you provide `SSH_KEY` secret, it will be added as a private SSH key to the home folder.
You can use this to install dependencies from private GitHub repositories or other private servers.

#### Upload test coverage files

If you need to upload test coverage files to Codecov.io or SonarCloud.io, you can use the following workflow inputs:

- `coverage_artifact_id` - artifact-id for GitHub actions/upload-artifact to store coverage report
- `coverage_path` - Path to coverage report that will be uploaded with coverage_artifact_id

#### Examples of usage

You can see the examples of usage of the poetry.yml workflow [here](https://github.com/search?q=org%3Asmg-real-estate%20public-workflows%2F.github%2Fworkflows%2Fpoetry.yml&type=code)
