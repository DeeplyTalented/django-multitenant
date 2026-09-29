## Contributing

This project welcomes contributions and suggestions. Most contributions
require you to agree to a Contributor License Agreement (CLA) declaring that
you have the right to, and actually do, grant us the rights to use your
contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine
whether you need to provide a CLA and decorate the PR appropriately (e.g.,
label, comment). Simply follow the instructions provided by the bot. You
will only need to do this once across all repositories using our CLA.

This project has adopted the [Microsoft Open Source Code of
Conduct](https://opensource.microsoft.com/codeofconduct/). For more
information see the [Code of Conduct
FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact
[opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional
questions or comments.

### Following our coding conventions

To format the python test files we use [black](https://github.com/psf/black).
After installing like this you can run the following before committing:
```bash
make format
```

You can also run the following to automatically format all the files that you
have changed before committing.

```bash
cat > .git/hooks/pre-commit << __EOF__
#!/bin/bash
black --check --quiet . || { black .; exit 1; }
__EOF__
chmod +x .git/hooks/pre-commit
```

### Running tests

In one shell start a PostgreSQL server with docker compose:
```bash
docker compose --project-name django-multitenant up -d || { docker compose logs && false ; }
```

Then in another shell run the tests (Django 6.0 requires Python 3.12 or newer):

```bash
export DJANGO_VERSION=6.0
make test-dependencies 
make test
```

The tests run against plain PostgreSQL by default. To also exercise the Citus-specific code paths
(table distribution, `citus.multi_shard_modify_mode`), run them with `USE_CITUS=1` against a Citus
cluster whose coordinator listens on `DATABASE_HOST`/`DATABASE_PORT` and whose workers are reachable as
`django-multitenant_worker1_1` and `django-multitenant_worker2_1` (see `tests/migrations/0002_distribute.py`).
