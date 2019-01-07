# Linux Ansible Virtual Environment

This Ansible role will create a python virtual environment containing Ansible, supporting python libraries, and the Azure python sdk (https://github.com/Azure/azure-sdk-for-python).

## Requirements

* The role defaults use magic variables. If accepting defaults, facts must be available.
* This role uses root to install system packages. Root is also used to create the virtual environment and required files/directories since the virtual environment is potentially being created for a user other than <code>ansible_user</code>. <code>ansible_user</code> must be able to sudo to root without a password.
* This role uses apt and pip to install packages. The host must have apt and pip sources setup.

## Role Variables

All over-writable variables used in this role are defined in defaults/main.yml.

You can override the variables in any standard Ansible-way (e.g. group_vars, host_vars, playbook variables, command-line, etc.).

The variables in this role include:

|parameter                 |required|default               |choices|comments|
|:-------------------------|:-------|:---------------------|:------|:-------|
|linux_ansible_venv_user   |false   |`{{ansible_user}}`    |       |The linux user that will own the virtual enviornment.|
|linux_ansible_venv_path   |false   |`{{ansible_user_dir}}`|       |The path to where the virtual environment will be installed. This should be a directory. The virtual environment will be named based on the version of Ansible installed.|
|linux_ansible_venv_version|false   |2.7.5                 |       |The version of Ansible that will be installed in the virtual environment. This must be a string. Note: Installing older versions of Ansible may cause package conflicts. Note: If there is a <code>-</code> in the ansible version name ex: <code>2.3.1.0-1</code>, use <code>2.3.1.0post1</code>.|
|linux_ansible_venv_apt    |false   |                      |       |A list of apt packages that will be installed. Checkout defaults/main.yml to see which packages will be installed. You probably don't want to modify this list unless you know what you are doing.|
|linux_ansible_venv_yum    |false   |                      |       |A list of yum packages that will be installed. Checkout defaults/main.yml to see which packages will be installed. You probably don't want to modify this list unless you know what you are doing.|
|linux_ansible_venv_pip    |false   |                      |       |A list of apt packages that will be installed in the python virtual environment. Checkout defaults/main.yml to see which packages will be installed. You probably don't want to modify this list unless you know what you are doing.|

## Example Playbook

Install Ansible virtual enviornment
```yaml
    - hosts: servers
      roles:
        - ar_linux_ansible_venv
```

## Author Information

|Author              |E-mail                   |
|:-------------------|:------------------------|
|Derek 'dRock' Halsey|derek.halsey@dinohead.com|

## License

MIT License

Copyright (c) 2019 Dinohead LLC

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Role Development Information

### Git SCM
Please refer to the .gitignore file and update accordingly depending on your
development environment, etc.  The particular file was generated at 
gitignore.io and contains settings for the following:
  - Ansible
  - Python
  - Vim
  - Eclipse
  - IntelliJ IDEA
  - Linux
  - Windows
  
### Versioning
Please update VERSION.md as you release new versions of your role and try to
abide by Semantic Versioning (compatibility).

Please consider using Gitflow such that individuals that want to use your role
can identify a version (e.g. master, develop, <tag>, etc.) to use.
  - https://danielkummer.github.io/git-flow-cheatsheet/
  - http://nvie.com/posts/a-successful-git-branching-model/

### Self-contained
Please try to keep this role as self-contained as possible such that it may be
simply installed (e.g. ansible-galaxy install) and applied as part of a 
playbook.
