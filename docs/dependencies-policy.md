# Dependencies Policy

* goal
  * how OpenFGA maintainers consume third-party packages

## Policy

TODO:
OpenFGA maintainers must follow these guidelines when consuming third-party packages:

- Only use third-party packages that are necessary for the functionality of OpenFGA.
- Use the latest version of all third-party packages whenever possible.
- Do not ue using third-party packages that are known to have security vulnerabilities.
- Pin all third-party packages to specific versions in the OpenFGA codebase.
- Use a dependency management tool, such as Go modules, to manage third-party dependencies.
- Integrate with monitoring tools to ensure that third-party packages are up-to-date and do not have security vulnerabilities.

## Procedure

When adding a new third-party package to OpenFGA, maintainers must follow these steps:

1. Evaluate the need for the package. Is it necessary for the functionality of OpenFGA? 
2. Research the package. Is it well-maintained? Does it have a good reputation? 
3. Choose a version of the package. Use the latest version whenever possible. 
4. Pin the package to the specific version in the OpenFGA codebase. 
5. Update the OpenFGA documentation to reflect the new dependency

## Credits

* inspired -- by -- [Kubescape Community](https://github.com/kubescape/kubescape/blob/master/docs/environment-dependencies-policy.md)