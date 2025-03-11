# Ansible Role: jsvc

[![CI](https://github.com/trfore/ansible-role-jsvc/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/trfore/ansible-role-jsvc/actions/workflows/ci.yml)
[![CD](https://github.com/trfore/ansible-role-jsvc/actions/workflows/cd.yml/badge.svg?branch=main)](https://github.com/trfore/ansible-role-jsvc/actions/workflows/cd.yml)

Compile the Apache Commons Daemon, aka `jsvc`, on RedHat/CentOS and Debian/Ubuntu.

This role downloads and compiles the latest source code from [Apache Commons (link)](https://dlcdn.apache.org/commons/daemon/source/),
and copies the binary to `/usr/bin/`. Optionally, it will remove the JDK and source code directory.

If you would like to manually download the source code to your Ansible control host, download the **native-src**,
`commons-daemon-*.*.*-native-src.tar.gz`, to your `files` directory and set the following two variables in your
playbook:

- `jsvc_tar_src: commons-daemon-*.*.*-native-src.tar.gz`
- `jsvc_tar_src_remote: false`

## Install the Role

You can install this role with the Ansible Galaxy CLI:

```bash
ansible-galaxy role install trfore.jsvc
```

You can also include it in a `requirements.yml` file and install it with `ansible-galaxy install -r requirements.yml`,
using the format:

```yaml
---
roles:
  - trfore.jsvc
```

## Tested Platforms

- `ansible-core` 2.16, 2.17 & 2.18
- `python` 3.10 & 3.11
- CentOS Stream 9
- Debian 11
- Ubuntu 22.04 & 24.04

## Requirements

None

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Variable                | Default                       | Description                                                                         | Required  |
| ----------------------- | ----------------------------- | ----------------------------------------------------------------------------------- | --------- |
| jsvc_src_version        | `1.4.1`                       | Apache Commons' Daemon latest release                                               | No        |
| jsvc_tar_src            | URL                           | Apache Commons' Daemon **native** source tar file, URL or relative path             | No        |
| jsvc_tar_hash           | URL                           | Apache Commons' Daemon **native** source tar hash file                              | No        |
| jsvc_tar_src_remote     | `true`                        | Boolean, `true` if downloading from URL                                             | No        |
| jsvc_tar_dir            | `/var/tmp`                    | Temporary directory on the target host for extracting and compiling the source code | No        |
| jsvc_tar_folder         | Automatic                     | Determined from the `jsvc_tar_src` variable                                         | Automatic |
| jsvc_build_dependencies | `["autoconf", "make", "gcc"]` | Packages for compiling the source code                                              | No        |
| jsvc_remove_jdk         | `false`                       | Boolean, uninstall the Java JDK after build                                         | No        |
| jsvc_remove_tar_folder  | `false`                       | Boolean, remove the source code temporary directory on the target host              | No        |

OS specific variables are listed below, along with default values (see `vars/main.yml`):

| Variable       | Default                        | Description       | Required |
| -------------- | ------------------------------ | ----------------- | -------- |
| jsvc_build_jdk | `openjdk-11-jdk-headless`      | Java JDK (Debian) | No       |
| jsvc_build_jdk | `java-11-openjdk-devel.x86_64` | Java JDK (RHEL)   | No       |

## Dependencies

None

## Example Playbook

```yaml
- hosts: servers
  become: true
  roles:
    - name: Compile jsvc binary
      role: trfore.jsvc
```

- If you manually download the tar file & wish to remove the JDK and source dir.

```yaml
- hosts: servers
  become: true
  vars:
    jsvc_tar_src: commons-daemon-1.4.1-native-src.tar.gz
    jsvc_tar_src_remote: false
    jsvc_remove_jdk: true
    jsvc_remove_tar_folder: true
  roles:
    - name: Compile jsvc binary
      role: trfore.jsvc
```

## License

This Ansible role is MIT.

Apache Commons Daemon (JSVC) is Apache License 2.0, for additional information see: <https://www.apache.org/licenses/>.

## Author Information

Taylor Fore (<https://github.com/trfore>)

## Related Roles & Playbooks

| Github                         | Ansible Galaxy           |
| ------------------------------ | ------------------------ |
| [ansible-role-jsvc]            | [trfore.jsvc]            |
| [ansible-role-mongodb-install] | [trfore.mongodb_install] |
| [ansible-role-omada-install]   | [trfore.omada_install]   |

## References

### Apache Commons Daemon / jsvc

- [Commons-Daemon]
- [Commons-Daemon Archive]
- [GitHub: Commons-Daemon]
- [Apache JIRA: Commons-Daemon Issue Tracker]

[ansible-role-jsvc]: https://github.com/trfore/ansible-role-jsvc
[trfore.jsvc]: https://galaxy.ansible.com/trfore/jsvc
[ansible-role-mongodb-install]: https://github.com/trfore/ansible-role-mongodb-install
[trfore.mongodb_install]: https://galaxy.ansible.com/trfore/mongodb_install
[ansible-role-omada-install]: https://github.com/trfore/ansible-role-omada-install
[trfore.omada_install]: https://galaxy.ansible.com/trfore/omada_install
[Apache JIRA: Commons-Daemon Issue Tracker]: https://issues.apache.org/jira/browse/DAEMON-*?jql=project%20%3D%20DAEMON
[Commons-Daemon]: https://commons.apache.org/proper/commons-daemon/jsvc.html
[Commons-Daemon Archive]: https://archive.apache.org/dist/commons/daemon/
[GitHub: Commons-Daemon]: https://github.com/apache/commons-daemon
