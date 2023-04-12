# Ansible Role: jsvc

[![ci](https://github.com/trfore/ansible-role-jsvc/workflows/ci/badge.svg?branch=main&event=push)](https://github.com/trfore/ansible-role-jsvc/actions/workflows/ci.yml)
[![cd](https://github.com/trfore/ansible-role-jsvc/actions/workflows/cd.yml/badge.svg?branch=main)](https://github.com/trfore/ansible-role-jsvc/actions/workflows/cd.yml)

Compile the Apache Commons Daemon, aka `jsvc`, on RedHat/CentOS, Debian/Ubuntu servers.

This role downloads and compiles the latest source code from Apache Commons, e.g. https://dlcdn.apache.org/commons/daemon/source/, and copies the binary to `/usr/bin/`. Optionally it will remove the JDK and source code directory.

If you would like to manually download the source code to your Ansible control host, download the **native-src**, `commons-daemon-*.*.*-native-src.tar.gz`, to your `files` directory and set the following two variables in your playbook:

- `jsvc_tar_src: commons-daemon-*.*.*-native-src.tar.gz`
- `jsvc_tar_src_remote: false`

### Install the Role

You can install this role with the Ansible Galaxy CLI:

```bash
ansible-galaxy role install trfore.jsvc
```

You can also include it in a `requirements.yml` file and install it with `ansible-galaxy role install -r requirements.yml`, using the format:

```yaml
---
roles:
  - trfore.jsvc
```

## Requirements

None

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Variable                | Default                       | Description                                                                         | Required  |
| ----------------------- | ----------------------------- | ----------------------------------------------------------------------------------- | --------- |
| jsvc_src_version        | Latest Release, `1.x.x`       | Apache Commons' Daemon version                                                      | Yes       |
| jsvc_tar_src            | URL                           | Apache Commons' Daemon **native** source tar file, URL or relative path             | Yes       |
| jsvc_tar_src_remote     | `true`                        | Boolean, `true` if downloading from URL                                             | Yes       |
| jsvc_tar_dir            | `/var/tmp`                    | Temporary directory on the target host for extracting and compiling the source code | Yes       |
| jsvc_tar_folder         | Automatic                     | Determined from the `jsvc_tar_src` variable                                         | Automatic |
| jsvc_build_dependencies | `["autoconf", "make", "gcc"]` | Packages for compiling the source code                                              | Yes       |
| jsvc_remove_jdk         | `false`                       | Boolean, uninstall the Java JDK after build                                         | Yes       |
| jsvc_remove_tar_folder  | `false`                       | Boolean, remove the source code temporary directory on the remote host              | Yes       |

OS specific variables are listed below, along with default values (see `vars/debian.yml` and `vars/redhat.yml`):

| Variable       | Default                        | Description       | Required |
| -------------- | ------------------------------ | ----------------- | -------- |
| jsvc_build_jdk | `openjdk-11-jdk-headless`      | Java JDK (Debian) | Yes      |
| jsvc_build_jdk | `java-11-openjdk-devel.x86_64` | Java JDK (RHEL)   | Yes      |

## Dependencies

None

## Example Playbook

```yaml
- hosts: servers
  roles:
    - name: Compile jsvc binary
      role: trfore.jsvc
```

- If you manually download the tar file & wish to remove the JDK and source dir.

```yaml
- hosts: servers
  vars:
    jsvc_tar_src: commons-daemon-1.3.3-native-src.tar.gz
    jsvc_tar_src_remote: false
    jsvc_remove_jdk: true
    jsvc_remove_tar_folder: true
  roles:
    - name: Compile jsvc binary
      role: trfore.jsvc
```

## License

MIT

## Author Information

[Taylor Fore](https://github.com/trfore)

## References

### Apache Commons Daemon / jsvc

- https://commons.apache.org/proper/commons-daemon/jsvc.html
- https://dlcdn.apache.org/commons/daemon/source/
- https://github.com/apache/commons-daemon
