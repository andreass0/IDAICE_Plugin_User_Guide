(Getting_started_with_the_RFem_Plugin)=

# Getting started with the IDA-ICE Plugin

## Installing the SIMULTAN-Editor

To use the plugin you need to install the latest version of the SIMULTAN Editor, which can be
found <strike>here</strike><!-- Da fehtl etwas -->. The SIMULTAN Editor enables you to interact
with the SIMULTAN data model through a user interface. A comprehensive user-guide how to install and interact with the
SIMULTAN Editor can be found under this [link](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki).

## Installing the IDA-ICE Plugin

After installing the SIMULTAN Editor you can install the IDA-ICE Plugin via the Plugin Manager {numref}`plugin_manager`.
Either download <!-- Aktualisiert -->the plugin from the SIMULTAN Server, `Plugin-Name: IDAICEPlugin`<!-- Hinzugefügt -->, or install from your local disk with the
installation file.

```{figure} img/plugin_manager.png
---
name: plugin_manager
---
Plugin Manager in the SIMULTAN Editor.
```

When the installation was successful a new tab will be added to your taskbar named `IDA ICE Plugin`
{numref}`idaice_plugin`. If Simultan is set to German, you can find it under the name `Neuer Ribbon Tab` at the moment.

```{figure} img/idaice_plugin.png
---
name: idaice_plugin
---
New tab added to the taskbar of the SIMULTAN Editor after installing the IDA-ICE Plugin.
```

## Run the example

To check if everything was installed properly please open `install_test_model.simultan` from the examples provided where
you [downloaded](files/install_test_model.simultan) the installation file of the plugin. Open the
example in your SIMULTAN Editor (username and password is "admin"), and follow the instructions in the
chapter [Running a simulation](Running_a_simulation.md). If this works fine and you are getting plausible results the
installation was successful. 