# Grout Schema Editor

A simple, static admin portal providing an interface to a Grout database.

## Requirements

The Grout Schema Editor is containerized with Docker for ease of use. In order
to develop with Docker, you need the following dependencies:

- [Docker CE Engine](https://docs.docker.com/install/) >= 1.13.0 (must be
  compatible with [Docker Compose file v3
  syntax](https://docs.docker.com/compose/compose-file/#compose-and-docker-compatibility-matrix))
- [Docker Compose](https://docs.docker.com/compose/install/)

## Use the schema editor in a project 

To incorporate the Grout Schema Editor into a project, clone it into your project
repo:

```
# Run this command in your project directory.
git clone git@github.com:azavea/grout-schema-editor.git
```

You can also manage the dependency using [git
subtree](https://www.atlassian.com/blog/git/alternatives-to-git-submodule-git-subtree)
if you plan to contribute your changes back upstream:

```bash
# Add the grout-schema-editor repo as a remote to your project directory.
git remote add -f grout-schema-editor git@github.com:azavea/grout-schema-editor.git

# Pull in grout-schema-editor as a subtree in your project.
git subtree add --prefix grout-schema-editor grout-schema-editor master
```

Next, copy and edit the example app config file to match the requirements of your project.
The default config values should be fine for most applications, with
the exception of `config.api.hostname`, which will likely need to be changed in order
to match the URI of your Grout database server instance:

```bash
# Move the example config file into the app directory.
cp example/config.js app/scripts/config.js
```

Finally, you'll have to run Grout server in parallel with your app so that
they can communicate with each other. For this purpose, we recommend
[Docker Compose](https://docs.docker.com/compose/). You can find an example
of a project that integrates an Grout server with Docker Compose in the
[Grout Blueprint](https://github.com/azavea/grout-blueprint) repo.

## Developing

You can set up a development environment for working on Grout Schema Editor
using the `update` script. (Note that the `update` script assumes you have
git installed with SSH set up. If you need an SSH key, refer to [the docs for generating
one](https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key).)

```bash
# Set up the development environment.
./scripts/update

# Create a local config file for the project.
cp example/config.js app/scripts/config.js
```

Next, use the `server` script to start the development server:

```bash
./scripts/server
```

This will run a Grout API server on `localhost:8000/api`, and the schema editor
app on `localhost:9000`.

## Testing

If you'd like to contribute to Grout Schema Editor, you can run tests using the
scripts located in the `scripts` directory:

```bash
# Build containers and install NPM modules.
./scripts/update

# Run tests.
./scripts/test
```
