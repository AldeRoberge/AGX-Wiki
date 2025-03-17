The services are built using GitHub Actions.

To test locally, we use [act](https://github.com/nektos/act).

```
act -W '.github/workflows/client-publish-googleplay.yml' -v --secret-file '.github/workflows/.secrets'
```







