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
tox -e py-ansible2.16-ubuntu20 run
# run all test in parallel
tox run-parallel
```

## Additional References

- [Ansible community guide](https://docs.ansible.com/ansible/devel/community/index.html)
- [Github Docs: Forking a repository](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo#forking-a-repository)
- [Ansible Docs: `ansible-core` support matrix](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#ansible-core-support-matrix)
