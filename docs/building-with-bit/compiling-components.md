---
id: compiling-components
title: Compiling
---

Compilation is a crucial step in making a component an independent module that can be used by other web projects as well as internally, by other components in the same workspace.
When Bit starts tracking a component, a new directory is created for it inside the workspace' `node_modules` directory. When a component gets compiled, the output of that process is placed inside the root of that directory.

For example:

```sh
├── node_modules
    ├── @my-org
        ├── react-ui.button
          ├── dist
              ├── index.js
              ├── index.js.map
              ├── button.js
              ├── button.js.map
          ├── ...
```

- **Compile in the workspace** - Components are compiled in 'watch mode' (on every change) when running Bit's dev server (`bit start`) and on various compilations commands.

- **Compile as a build task** -
  Components are compiled as part of the component build pipeline (on `bit build` and `bit tag`).
  The compilation task runs on the component's 'capsule' (generated as part of the build process) and not on the workspace.
  Since the build pipeline runs not only on the modified components but also on all dependents of that component, so does the the compilation process.

## Choosing a Compiler

Bit's Compiler is an Environment Service.
The type of compiler (Babel, TypeScript, etc.) as well as its configurations, are set by the various [environments](/building-with-bit/environments) that use it as a service.
That means, the (specific) compiler is never run directly but only via the Compiler service. That also means, a single workspace may run different compilers for different components, each according to its own environment.
To customize an environment's compiler, [see here](/building-with-bit/environments).

## Running the compiler manually

To manually run the compiler on a specific component use its component ID

```shell
bit compile <component-id>
```

For example:

```shell
bit compile ui-primitives/button
```

To manually run the compiler on the entire workspace:

```shell
bit compile
```

### Options

#### `--changed` `-c`

Compiles only new or modified components.

```shell
bit compile --changed
```

#### `--verbose` `-v`

Outputs data regarding the compilation. For example, the `dist` paths.

```shell
bit compile --verbose
```

#### `--json` `-j`

Outputs (to the terminal) the compiled results in a JSON format.

```shell
bit compile --json
```

## Bit processes that use the compiler

### Local dev server

Bit's local dev server (which also runs the Workspace UI) re-compiles components on each modification. This happens whenever a file is 'saved'.

```shell
bit start
ENVIRONMENT NAME        URL                      STATUS
react              http://localhost:3101         Running
node               http://localhost:3102         Running

You can now view bad-jokes components in the browser
Main UI server is running on http://localhost:3000

Waiting for component changes... (10:17:20)
```

### Compile in `watch` mode

Alongside the local dev server, Bit features a watch mode that runs different operations for modified components. Component compilation is one of these tasks.

```sh
bit watch
```

- __Compile in the workspace__ - Components are compiled in 'watch mode' (on every change) when running Bit's dev server (`bit start`) and on various compilations commands.


- __Compile as a build task__ - 
Components are compiled as part of the component build pipeline (on `bit build` and `bit tag`).
The compilation task runs on the component's 'capsule' (generated as part of the build process) and not on the workspace.
Since the build pipeline runs not only on the modified components but also on all dependents of that component, so does the the compilation process.

```
$ bit watch
```

### Compile in the Build Pipeline

Compilation is also part of a component's build pipeline. As with any other Build Task, the compilation task also happens in a 'component capsule', which is an isolated instance of a component. When executed as a Build Task, the compiler processes all new or changed dependencies of that component.

When a component's build pipeline is run as part of the tagging of a new release version, the output of the compilation process is stored in the component's new version.
