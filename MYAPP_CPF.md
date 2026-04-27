# What `myapp.cpf` Is For

This document is only an explanation of the template configuration. You do not need to run these lines manually during deployment.

`myapp.cpf` is a configuration merge file for InterSystems IRIS. During the Docker image build, the Dockerfile runs:

```bash
iris merge IRIS /tmp/myapp.cpf
```

That command applies the settings from `myapp.cpf` to the IRIS instance. In this template, the file creates the application namespace, enables interoperability support, and defines the web applications used by the UI and REST API.

## `myapp.cpf` Actions

```ini
[Actions]
```

Starts the configuration merge actions section. The lines below it are executed by IRIS during the merge.

```ini
CreateDatabase:Name=MYAPP,Directory=/usr/irissys/mgr/MYAPP
```

Creates the `MYAPP` database in `/usr/irissys/mgr/MYAPP`. This database stores the application globals and routines.

```ini
CreateNamespace:Name=MYAPP,Globals=MYAPP,Routines=MYAPP,Interop=1
```

Creates the `MYAPP` namespace. It uses the `MYAPP` database for globals and routines. `Interop=1` enables the namespace for InterSystems interoperability productions.

```ini
CreateDatabase:Name=MYAPP_DATAENSTEMP,Directory=/usr/irissys/mgr/MYAPP_DATAENSTEMP
```

Creates an additional database used by interoperability-related configuration.

```ini
CreateDatabase:Name=MYAPP_DATASECONDARY,Directory=/usr/irissys/mgr/MYAPP_DATASECONDARY
```

Creates another additional database used by interoperability-related configuration.

```ini
CreateApplication:Name=/myapp,NameSpace=MYAPP,Path=/usr/irissys/csp/myapp,CSPZENEnabled=1,Enabled=1,ServeFiles=1,AutheEnabled=64,Recurse=1
```

Creates the `/myapp` web application. It serves files from `/usr/irissys/csp/myapp`, which is where the Dockerfile copies the `web` folder. `ServeFiles=1` allows static files such as `index.html` to be served.

```ini
CreateApplication:Name=/myapp/api,NameSpace=MYAPP,DispatchClass=Sandbox.Cloudsample.REST,CSPZENEnabled=1,Enabled=1,AutheEnabled=64,MatchRoles=:%All
```

Creates the `/myapp/api` REST application. Requests are dispatched to `Sandbox.Cloudsample.REST`. In this template, `GET /myapp/api/test` returns a JSON status response. `MatchRoles=:%All` adds the `%All` application role while the request is handled by this application.
