# Yandex Open Source Jam 2024

1\. Установка [git](https://git-scm.com/downloads)

{% list tabs %}

- macOS

  ```
  brew install git
  ```
- Linux/Unix

  ```
  apt-get install git
  ```
- Windows

  ```
  winget install --id Git.Git -e --source winget
  ```
  
{% endlist %}

2\. Установка [GitHub CLI](https://github.com/cli/cli)

{% list tabs %}

- macOS

  ```
  brew install gh
  ```
- Linux/Unix

    ```
    (type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
    && sudo mkdir -p -m 755 /etc/apt/keyrings \
    && wget -qO- https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
    && sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && sudo apt update \
    && sudo apt install gh -y
    ```
- Windows

  ```
  winget install --id GitHub.cli
  ```
  
{% endlist %}

3\. [Репозиторий воркшопа](https://github.com/diplodoc-platform/notconf-steps)
4\. Основные шаги:
```bash
function step { rm -rf ./**; cp -fr ../steps/step-$1/ .; }

git clone git@github.com:diplodoc-platform/notconf-steps.git steps
# create <docs-example> gh project from scratch
gh repo create
cd docs-example

# install our cli as an gh extension, may take some take
gh extension install diplodoc-platform/gh-docs
```
