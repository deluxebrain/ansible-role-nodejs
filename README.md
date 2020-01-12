# Role Name: NODEJS

[![Build Status](https://travis-ci.org/deluxebrain/ansible-role-nodejs.svg?branch=master)](https://travis-ci.org/deluxebrain/ansible-role-nodejs)

NodeJS installer for Linux.
Includes node-build and nodenv-vars plugins by default for installing Node.js versions and per-project environment variables respectively.

## Requirements

None.

## Role Variables

All of the listed variables are defined in `defaults/main.yml`.
Individual variables can be set or overridden by setting them in a playbook for this role.

- `nodenv_version`: ( default: latest )
  - nodenv version to install
- `nodebuild_version`: ( default: latest )
  - node-build version to install
- `nodenvvars_version`: ( default: latest )
  - nodenv-vars version to install
- `init_shell`: ( default: yes )
  - Configure shell to load nodenv
- `nodejs.default_version`: ( default: "" )
  - Version of Node.js to use by default
- `nodejs.versions`: ( default: [] )
  - List of Node.js versions to install
- `plugins`: ( default: [] )
  - List of plugins to install, specified as a list of:
    - `name`: plugin name
    - `repo`: plugin github repository
    - `version`: plugin version, specify "latest" for HEAD

## Dependencies

None.

## Example Playbook

Example below for the following:

- Installation of specific versions of `nodenv`
- Installation of specific version of Node.js
- Installation of the `nodenv-default-packages` nodenv plugin

```yaml
- hosts: servers
  roles:
      - deluxebrain.python
        nodenv_version: 1.3.1
        nodejs:
          default_version: 12.3.1
          versions:
            - 12.3.1
          plugins:
            - name: nodenv-default-packages
              repo: https://github.com/nodenv/nodenv-default-packages.git
              version: latest
```

## Usage

### `nodenv`

`nodenv` allows you to use multiple Node versions on your machine.

```sh
# Install specific Node version
nodenv install 12.3.1

# Create project directory
mkdir ~/my-project && cd $_

# Configure the project to use specific Node version
nodenv local 12.3.1   # creates .node-version
```

### `npm`

The use of npm for creating a new project is demonstated in the following example:

```sh
npx license mit > LICENSE     # Generate license file
npx gitignore node            # Specify .gitignore
npx covgen <EMAIL_ADDRESS>    # Specify Code of Conduct email address
npm init -y                   # Initialize project
npm install <package>
```

Note that `npx` should be used in preference to installing packages globally.

### `nodenv-vars`

`nodenv-vars` is a plugin for `nodenv` that allow for per-project application environment variables.

Its use is demonstrated in the following example:

```sh
echo FOO=BAR >> .nodenv-vars
$ nodenv vars
export FOO='BAR'
```

## License

MIT / BSD

## Author Information

This role was created in 2020 by [deluxebrain](https://www.deluxebrain.com/).
