# QuecPython Project Manager User Guide

## Overview

- This package manager is based on a git repository and can access repositories under the QuecPython organization or other specified organizations on GitHub.

- When the user specifies the package name instead of the URL, it defaults to accessing the QuecPython organization on GitHub, managing packages released by QuecPython.

- Users can reconfigure the GitHub organization through the `config` command to manage packages under their own organization.

- The package manager does not make local commits for the project; users need to decide what content to commit via the `git commit` command. However, the package manager can publish the package to the server and specify the release version.

## Commands

`qpm` is a command-line tool for managing QuecPython projects. It provides functionalities for creating, initializing, importing, adding, removing, publishing, listing, showing versions, deploying, and configuring projects.

### Version Information

```bash
qpm -v, --version
```

Displays the version information of the tool.

### Help Information

```bash
qpm [help | -h, --help]
```

Displays help information.

### Create a New Project

```bash
qpm new [-h] [-u URL] proj_name
```

**-h, --help**: Show help information for the `new` command.  
**-u, --upstream URL**: Add the URL of the remote repository (optional).  
**proj_name**: Project name.

### Initialize the Current Directory as a QuecPython Project

```bash
qpm init [-h] [-u URL]
```

**-h, --help**: Show help information for the `init` command.  
**-u, --upstream URL**: Add the URL of the remote repository (optional).

### Import a Project

```bash
qpm import [-h] [-v version] proj_name_or_url
```

**-h, --help**: Show help information for the `import` command.  
**-v, --version version**: Project version (optional).  
**proj_name_or_url**: Project name or URL.

### Add a Dependency Package

```bash
qpm add [-h] [-v version] pkg_name_or_url path
```

**-h, --help**: Show help information for the `add` command.  
**-v, --version version**: Package version (optional).  
**pkg_name_or_url**: Package name or URL.  
**path**: Package path.

### Remove a Dependency Package

```bash
qpm remove [-h] [pkg_path]
```

**-h, --help**: Show help information for the `remove` command.  
**pkg_path**: Package path (optional).

### Publish the Current Package

```bash
qpm publish [-h] [-v version] [-m message] [-d version]
```

**-h, --help**: Show help information for the `publish` command.  
**-v, --version version**: Version to be published.  
**-m, --message message**: Message for the release version (optional).  
**-d, --delete version**: Delete the published version.

### List Local or Remote Package Information

```bash
qpm ls [-h] [-l] [-r] [-p remote_pkg_name] [-v version]
```

**-h, --help**: Show help information for the `ls` command.  
**-l, --local**: List local package information.  
**-r, --remote**: List remote packages.  
**-p, --package remote_pkg_name**: List dependencies of the remote package.  
**-v, --version version**: Version of the remote package to list (optional).

### Show All Versions of a Local or Remote Package

```bash
qpm release [-h] [pkg_name_or_url]
```

**-h, --help**: Show help information for the `release` command.  
**pkg_name_or_url**: Package name or URL (optional).

### Deploy a Project or Package

```bash
qpm deploy [-h] [-v version]
```

**-h, --help**: Show help information for the `deploy` command.  
**-v, --version version**: Version of the project or package (optional).

### View Package Version

```bash
qpm version [-h]
```

**-h, --help**: Show help information for the `version` command.

### Configure the Project

```bash
qpm config [-h] [-g] key [value]
```

**-h, --help**: Show help information for the `config` command.  
**-g, --global-config**: Global configuration (optional).  
**key**: Key of the configuration item.  
**value**: Value of the configuration item (optional).

> - The priority of project configuration, from high to low, is: Local Configuration > Global Configuration > Default Configuration.
> - User's local or global configuration will override the default configuration.
> - The package manager is pre-configured with QuecPython as the GitHub organization and the corresponding access token.

---

## Examples

### Create a New Project

```bash
# Without associating a remote repository URL
qpm new project

# Associating a remote repository URL
qpm new project -u https://github.com/user/repo.git
```

### Initialize the Current Directory as a QuecPython Project

```bash
# Without associating a remote repository URL
qpm init

# Associating a remote repository URL
qpm init -u https://github.com/user/repo.git
```

### Import a Project

```bash
# Import project by package name without specifying the project version
qpm import project

# Import project by package name and specify the project version
qpm import project -v 1.0.0

# Import project by URL without specifying the project version
qpm import https://github.com/user/repo.git

# Import project by URL and specify the project version
qpm import https://github.com/user/repo.git -v 1.0.0
```

### Add a Dependency Package

```bash
# Add a dependency package by name without specifying the package version
qpm add package /path/to/package

# Add a dependency package by name and specify the package version
qpm add package /path/to/package -v 2.25.1

# Add a dependency package by URL without specifying the package version
qpm add https://github.com/user/repo.git /path/to/package

# Add a dependency package by URL and specify the package version
qpm add https://github.com/user/repo.git /path/to/package -v 2.25.1
```

### Remove a Dependency Package

```bash
# Remove a specified dependency package
qpm remove /path/to/package

# Remove all dependency packages
qpm remove
```

### Publish the Current Package

```bash
# Publish the current package without specifying version message
qpm publish -v 1.0.0

# Publish the current package with a version message
qpm publish -v 1.0.0 -m "Initial release"

# Delete the published version
qpm publish -d v1.0.0
```

### List Local or Remote Package Information

```bash
# List the dependency tree of local packages
qpm ls
qpm ls -l

# List all packages under the GitHub organization
qpm ls -r

# List dependencies of a specified package under the GitHub organization without specifying the package version
qpm ls -p package

# List dependencies of a specified package under the GitHub organization and specify the package version
qpm ls -p package -v v1.2.0
```

### Show All Versions of a Local or Remote Package

```bash
# View all versions of the currently published local package
qpm release

# View all versions of a specified package under the GitHub organization by package name
qpm release package

# View all versions of a package by URL
qpm release https://github.com/user/repo.git
```

### Deploy a Project or Package

```bash
# Without specifying the version
qpm deploy

# Specifying the version
qpm deploy -v 1.0.0
```

### View Package Version

```bash
qpm version
```

### Configure the Project

```bash
# Set local configuration
qpm config key value

# Query local configuration
qpm config key

# Set global configuration
qpm config -g key value

# Query global configuration
qpm config -g key

# Configure local GitHub organization
qpm config github_organization your_github_organization

# Configure local GitHub access token
qpm config github_access_token your_github_access_token

# Configure global GitHub organization
qpm config -g github_organization your_github_organization

# Configure global GitHub access token
qpm config -g github_access_token your_github_access_token
```

## Notes

- When executing certain commands, the tool will check if the current directory is within a QuecPython project. If the conditions are not met, the tool will print an error message and exit.