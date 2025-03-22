# Contributing

## Contribute

### Setup a Dev Environment

```sh
python3 -m venv .venv && source .venv/bin/activate
python3 -m pip install -r requirements/dev-requirements.txt
pre-commit install
```

### Running Test

- Pre-commit commands:

```sh
pre-commit run --all-files
```

- Tox commands:

```sh
# list environments and test
tox list

# lint all files
tox -e lint run

# run a specific test environment
tox -e py-ansible2.17-ubuntu22-default run

# run all test in parallel
tox run-parallel

# changing the downloaded JSVC version
JSVC_VERSION='1.4.0' tox -e py-ansible2.17-ubuntu22-default run
```

### Advance Dev/Testing: Molecule commands within Tox venv

```bash
tox -e py-ansible2.17-ubuntu22-default run -- test -s default --destroy=never
tox -e py-ansible2.17-ubuntu22-default run -- destroy
```

## Additional References

- [Ansible community guide](https://docs.ansible.com/ansible/devel/community/index.html)
- [Ansible Docs: `ansible-core` support matrix](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#ansible-core-support-matrix)
- [Github Docs: Forking a repository](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo#forking-a-repository)
- [RHEL: OpenJDK Life Cycle and Support Policy](https://access.redhat.com/articles/1299013)
