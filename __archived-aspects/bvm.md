---
id: bvm
title: BVM
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

[BVM](https://github.com/teambit/bvm) is a version manager for Bit.  
Using BVM makes it easier to install and manage multiple versions of Bit in a single environment.

### Features

- __Consistent installation:__ All Bit dependencies are bundled together to ensure a consistent and predictable package installation that is not affected by SemVer rules.
- __Fast installation:__ A simple and quick installation process that requires no additional time-consuming operations (post-install scripts, etc.)
- __Friendly UX:__ Easy upgrades and version management
- __Multiple Bit versions:__ Easily switch between Bit versions or even use multiple versions in parallel

### Install BVM

<Tabs
  defaultValue="NPM"
  values={[
    {label: 'NPM', value: 'NPM'},
    {label: 'Yarn', value: 'Yarn'},
  ]}>
  <TabItem value="NPM">

```shell
npm i -g @teambit/bvm
```

  </TabItem>
  <TabItem value="Yarn">

```shell
yarn global add @teambit/bvm
```

  </TabItem>
</Tabs>

### Install Bit
#### Install Bit's latest version
```shell
bvm install
```

#### Install A specific Bit version
```shell
bvm install <bit-version>
```
#### Upgrade to Bit's latest version
Install the latest version and remove the version previously used.
```shell
bvm upgrade
```

### Manage versions

#### Get the current version of BVM
```shell
bvm -v
```

#### List all versions of BVM available to be installed
```shell
bvm list --remote
```

#### Get the local and remote versions of Bit and BVM
Get the local used versions, local latest versions and remote latest versions of Bit and BVM
```shell
bvm version
```

#### List all installed Bit versions
```shell
bvm list
```

#### Remove an installed Bit version
```shell
bvm remove <bit-version>
```

#### Link to a specific Bit version
Link a command name to a Bit version (link to binaries in the `PATH` variable).

```shell
bvm link <command> <bit-version>
```

For example, the following line will link Bit's version `0.0.315` to the `bitty` command name
(this will execute Bit's version `0.0.315` whenever the `bitty` command is used).
```
bvm link bitty 0.0.315
```
Validate the link by checking the version number of the new link:
```shell
$ bitty -v

0.0.315 (@teambit/legacy: 1.0.28)
```

:::info Auto-Link Bit's latest version to `bbit`
If a legacy version of Bit (Bit v14) is installed on your machine,
BVM will automatically link the latest version to `bbit` (instead of `bit`) to allow you to use both versions in parallel.
:::

### BVM configurations

#### Get BVM configurations

- `DEFAULT_LINK` -  The default command name to be linked to BVM's latest version.  
`bit` is linked by default unless a legacy version of Bit is installed. In that case, `bbit` will be linked, instead.

- `BVM_DIR` -  The location for BVM

```shell
bvm config
```

#### Set BVM configurations

```shell
bvm config set <property> <new-value>
```

For example, to change the default link for Bit, from  `bit` to `bitty`:

```shell
bvm config set DEFAULT_LINK bitty
```



### Troubleshooting

#### PATH is missing the installation directory

- [Installation Troubleshooting](/troubleshooting/installation-troubleshooting).