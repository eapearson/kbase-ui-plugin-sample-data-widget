# KBase UI Plugin - Sample Data Widget

A sample kbase-ui plugin containing data widgets and configuration for incorporating them into the dataview landing page.

## Getting Started

- create a local development directory
- within that directory:
- fork and clone the develop branch of https://github.com/kbase/kbase-ui
    - ```git clone -b develop https://github.com/someuser/kbase-ui```
- clone this repo https://github.com/eapearson/kbase-ui-plugin-sample-data-widget
- rename the sample-data-widget directory to whatever you want, say kbase-ui-plugin-my-plugin
    - to wit ```git clone https://github.com/eapearson/kbase-ui-plugin-sample-data-widget kbase-ui-plugin-my-plugin```
- within kbase-ui-plugin-my-plugin
- remove the .git directory
- edit the bower.json and package.json files to modify the name property to reflect this change
- edit src/plugin/config.yml to change all occurrences of sample-data-widget to my-plugin

### First Build

Before integrating the plugin, ensure that kbase-ui will build and run

Within the kbase-ui directory:

```
make init
make build
make start
make preview
```

### Integrate Plugin

Within the kbase-ui directory:

- copy the config directory into the dev directory
- edit  dev/config/link.sh to create a link to the my-plugin repo.
  - in the EXTERNAL PLUGINS section, uncomment the two example lines
```
# rm -rf ../../build/build/client/modules/plugins/PLUGIN
# ln -s /DEVDIR/kbase-ui-plugin-PLUGIN/src/plugin ../../build/build/client/modules/plugins/PLUGIN
```
  - replace PLUGIN with my-plugin, and DEVDIR with the absolute path to the plugin directory.

- edit dev/config/ui/dev/build.yml
- at the end of the plugins section add a section like this:

```
    -
        name: my-plugin
        globalName: kbase-ui-plugin-my-plugin
        version: 0.1.0
        cwd: src/plugin
        source:
            directory:
                path: /DEVDIR/kbase-ui-plugin-my-plugin/src/plugin
```

- edit dev/config/ui/dev/settings.yml
- in the menu.authenticated property add the menu item sample-contigset to the list of menu items.

### Build with the plugin

Back in kbase-ui, rebuild kbase-ui, but this time including the plugin:

```
make build; cd dev/config; sh link.sh; cd ../..
```

You should now see the menu item "Sample - ContigSet" in the hamburger menu

### Here is what you now have:

- menu item sample-contigset, which invokes panel.js, which embeds several sample widgets, including contigset.
- data widgets for contigset and proteome comparison
- type mappings for those two widets so that they are activated on the dataview landing page

### Further Fun

- use the type browser to locate the contigset or proteome comparison types, browse to existing objects, and load the landing page to see the included widgets.
- play with the widgets, reload the landing page, and see the effects.

### Integrating your widgets

The Proteome Comparison widget located in src/plugin/modules/kbaseGenomeComparison is an example of a jquery-based kbwidget. See this file, and the configuration of it in src/plugin/config.yml.