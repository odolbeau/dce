# DCE

DCE stands for Docker ComposE or Docker Compose Extended.
The goal is to simplify the usage of the docker compose commands when using several Compose configuration files or options.
The command will read the `.dcerc` configuration file if present in order to automatically add desired options to the `docker compose` command.

## Installation

Simply copy the `dce` command of this repository in a folder which is present in your $PATH.

```bash
sudo sh -c 'curl -s https://raw.githubusercontent.com/odolbeau/dce/master/dce > /usr/local/bin/dce && chmod +x /usr/local/bin/dce'
```

In order to install bash_completion:

```bash
sudo sh -c 'curl -s https://raw.githubusercontent.com/odolbeau/dce/master/bash_completion > /etc/bash_completion.d/dce'
```

## Usage

### Automatically add options using a `.dcerc` file.

In a project which contains several compose configuration files, you can create a `.dcerc` file like this one:

```
# Give a name to this project (instead of using the current directory name)
-p my_project name

# includes all needed compose configuration files
-i docker/services/traefik.yml
-i docker/websites/blog.yml
-i docker/websites/another_blog.yml

# Include some secrets stored in a specific env file
--env-file .secrets
```

Then simply call the `dce` command and you're done! 👌
Ship this file in your repository to ensure your collaborators use exactly the same config than you!

### Dealing with environment files

By default, `dce` will include `.env` and `.env.prod` files if present in the current folder. You can change the default environment used by `dce` by creating a `~/.config/dce/env` file. For example, if this file contains "local", `dce` will automatically includes `env` and `.env.local` files if it exists.

## Improvements

Use `--project-directory` option when provided to look for a .dcerc file in the given folder
