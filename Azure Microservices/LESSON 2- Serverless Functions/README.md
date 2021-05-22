# Lesson 2

## Course Outline

```
az functionapp create \
--resource-group "azure-functions-udacity" \
--name "function-app-demo-nayanexx" \
--storage-account "udacity0function0demo" \
--os-type Linux \
--consumption-plan-location "westeurope" \
--runtime python
```

[Azure CLI Documentation - az functionapp](https://docs.microsoft.com/en-us/cli/azure/functionapp?view=azure-cli-latest#az_functionapp_create)


`az account list-locations --output=table`

## Pipenv

First, let’s install it:

```
pip install pipenv
```

Once you’ve done that, you can effectively forget about pip since Pipenv essentially acts as a replacement. It also introduces two new files, the `Pipfile` (which is meant to replace `requirements.txt`) and the `Pipfile.lock` (which enables **deterministic builds)**.

`Pipenv` uses `pip` and `virtualenv` under the hood but simplifies their usage with a single command line interface.

### Example Usage

First, spawn a shell in a virtual environment to isolate the development of this app:

Activate virtualenv:

`pipenv shell`

This will create a virtual environment if one doesn’t already exist. Pipenv creates all your virtual environments in a default location. If you want to change Pipenv’s default behavior, there are some [environmental variables for configuration](https://docs.pipenv.org/advanced/#configuration-with-environment-variables).

You can force the creation of a Python 2 or 3 environment with the arguments `--two` and `--three` respectively. Otherwise, Pipenv will use whatever default virtualenv finds.

> Sidenote: If you require a more specific version of Python, you can provide a --python argument with the version you require. For example: --python 3.6

Now you can install the 3rd party package you need. If you know that you need version 0.12.1 and not the latest version, go ahead and be specific:

```
pipenv install flask==0.12.1
pipenv install numpy
```

You’ll notice that two files get created, a `Pipfile` and `Pipfile.lock`.

If you want to install something directly from a version control system (VCS), you can! You specify the locations similarly to how you’d do so with pip. For example, to install the requests library from version control, do the following:

```
pipenv install -e git+https://github.com/requests/requests.git#egg=requests
```

Note the `-e` argument above to make the installation **editable**. Currently, this is required for Pipenv to do **sub-dependency resolution**.

Let’s say you also have some unit tests, and you want to use `pytest`. You don’t need `pytest` in production so you can specify that this dependency is only for **development** with the `--dev` argument:

```
pipenv install pytest --dev
```

Providing the `--dev` argument will put the dependency in a special [dev-packages] location in the Pipfile. These development packages only get installed if you specify the --dev argument with pipenv install.

The different sections separate dependencies needed only for development from ones needed for the base code to actually work. Typically, this would be accomplished with additional requirements files like `dev-requirements.txt` or `test-requirements.txt`. Now, everything is consolidated in a single Pipfile under different sections.

Okay, so let’s say you’ve got everything working in your local development environment and you’re ready to push it to production. To do that, you need to **lock your environment** so you can ensure you have the same one in production:

```
pipenv lock
```

This will create/update your `Pipfile.lock`, which you’ll never need to (and are never meant to) edit manually. **You should always use the generated file**.

Now, once you get your code and `Pipfile.lock` in your production environment, you should install the last successful environment recorded:

```
pipenv install --ignore-pipfile
```

This tells Pipenv to ignore the Pipfile for installation and use what’s in the `Pipfile.lock`. Given this `Pipfile.lock`, Pipenv will create the exact same environment you had when you ran pipenv lock, sub-dependencies and all.

The lock file enables deterministic builds by taking a snapshot of all the versions of packages in an environment (similar to the result of a `pip freeze`).

Now let’s say another developer wants to make some additions to your code. In this situation, they would get the code, including the Pipfile, and use this command:

```
pipenv install --dev
```

This installs all the dependencies needed for development, which includes both the regular dependencies and those you specified with the `--dev` argument during install.

> When an exact version isn’t specified in the Pipfile, the install command gives the opportunity for dependencies (and sub-dependencies) to update their versions.

This is an important note because it solves some of the previous problems we discussed. To demonstrate, let’s say a new version of one of your dependencies becomes available. Because you don’t need a specific version of this dependency, you don’t specify an exact version in the Pipfile. When you `pipenv install`, the new version of the dependency will be installed in your development environment.

Now you make your changes to the code and run some tests to verify everything is still working as expected. Now, just as before, you lock your environment with `pipenv lock`, and an updated `Pipfile.lock` will be generated with the new version of the dependencies. Just as before, you can replicate this new environment in production with the lock file.

As you can see from this scenario, you no longer have to force exact versions you don’t truly need to ensure your development and production environments are the same. You also don’t need to stay on top of updating sub-dependencies you “don’t care about.” This workflow with Pipenv, combined with your excellent testing, fixes the issues of manually doing all your dependency management.

### The Pipfile

`Pipfile` intends to replace `requirements.txt`. Pipenv is currently the reference implementation for using Pipfile. It seems very likely that pip itself will be able to handle these files. Also, it’s worth noting that Pipenv is even the official package management tool recommended by Python itself.

The syntax for the Pipfile is TOML, and the file is separated into sections. [dev-packages] for development-only packages, [packages] for minimally required packages, and [requires] for other requirements like a specific version of Python. See an example file below:

Config file:

```toml
[[source]]
url = "https://pypi.python.org/simple"
verify_ssl = true
name = "pypi"

[dev-packages]
pytest = "*"

[packages]
flask = "==0.12.1"
numpy = "*"
requests = {git = "https://github.com/requests/requests.git", editable = true}

[requires]
python_version = "3.6"
```

Ideally, you shouldn’t have any sub-dependencies in your Pipfile. What I mean by that is you should only include the packages you actually import and use. No need to keep chardet in your Pipfile just because it’s a sub-dependency of requests. (Pipenv will install it automatically.) The Pipfile should convey the top-level dependencies your package requires.

### The Pipfile.lock

This file enables deterministic builds by specifying the exact requirements for reproducing an environment. It contains exact versions for packages and hashes to support more secure verification, which pip itself now supports as well. An example file might look like the following. Note that the syntax for this file is JSON and that I’ve excluded parts of the file with ...:

```json
{
    "_meta": {
        ...
    },
    "default": {
        "flask": {
            "hashes": [
                "sha256:6c3130c8927109a08225993e4e503de4ac4f2678678ae211b33b519c622a7242",
                "sha256:9dce4b6bfbb5b062181d3f7da8f727ff70c1156cbb4024351eafd426deb5fb88"
            ],
            "version": "==0.12.1"
        },
        "requests": {
            "editable": true,
            "git": "https://github.com/requests/requests.git",
            "ref": "4ea09e49f7d518d365e7c6f7ff6ed9ca70d6ec2e"
        },
        "werkzeug": {
            "hashes": [
                "sha256:d5da73735293558eb1651ee2fddc4d0dedcfa06538b8813a2e20011583c9e49b",
                "sha256:c3fd7a7d41976d9f44db327260e263132466836cef6f91512889ed60ad26557c"
            ],
            "version": "==0.14.1"
        }
        ...
    },
    "develop": {
        "pytest": {
            "hashes": [
                "sha256:8970e25181e15ab14ae895599a0a0e0ade7d1f1c4c8ca1072ce16f25526a184d",
                "sha256:9ddcb879c8cc859d2540204b5399011f842e5e8823674bf429f70ada281b3cc6"
            ],
            "version": "==3.4.1"
        },
        ...
    }
}
```

Note the exact version specified for every dependency. Even the sub-dependencies like werkzeug that aren’t in our Pipfile appear in this Pipfile.lock. The hashes are used to ensure you’re retrieving the same package as you did in development.

It’s worth noting again that you should never change this file by hand. It is meant to be generated with pipenv lock.

### Pipenv Extra Features

Check for security vulnerabilities (and PEP 508 requirements) in your environment:

`pipenv check``

Now, let’s say you no longer need a package. You can uninstall it:

`pipenv uninstall numpy``

Additionally, let’s say you want to completely wipe all the installed packages from your virtual environment:

`pipenv uninstall --all`

You can replace `--all` with `--all-dev` to just remove dev packages.

Pipenv supports the automatic loading of environmental variables when a `.env` file exists in the top-level directory. That way, when you `pipenv shell` to open the virtual environment, it loads your environmental variables from the file. 

```
SOME_ENV_CONFIG=some_value
SOME_OTHER_ENV_CONFIG=some_other_value
```

Finally, here are some quick commands to find out where stuff is. How to find out where your virtual environment is:

`pipenv --venv`

How to find out where your project home is:

`pipenv --where`



### Other Resources/Documentation about Pipenv <3

[Pipenv Docs](https://docs.pipenv.org/)
[Pipenv Latest](https://pipenv.pypa.io/en/latest/)
[Pipenv Basics](https://pipenv-fork.readthedocs.io/en/latest/basics.html)
[Pipenv Install](https://pipenv-fork.readthedocs.io/en/latest/install.html)
[The Hitchhikers's Guide do Pipenv](https://docs.python-guide.org/dev/virtualenvs/)
[Configure Pipenv in PyCharm](https://www.jetbrains.com/help/pycharm/pipenv.html)
[Real Python - Pipenv Guide](https://realpython.com/pipenv-guide/)
[Managing Application Dependencies](https://packaging.python.org/tutorials/managing-dependencies/#managing-dependencies)
