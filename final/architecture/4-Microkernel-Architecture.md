It have a central then plugin a feature to the core.
# Topology
Having a core and plugin. It must have a core function to run the system. It can called **happy path**.

Inside the core can be layered and modular architecture. Also can having a frontend to attach to the core.
## Plugin
The plugin must be independent to another plugin. and isolate standalone.
- Runtime plugin: We can change the plugin during runtime.
- Compile-based plugin: During compile.
Also we can do a remote plugin that (from internet)

Make it loose the coupling but complex
## Registry
To connect the plugin and core used to know that what plugin do
contracts (plugin interface),
## Data Topology
Each plugin can have a database. 1 Database per service 
## Risks
If core is change บ่อย it will effect every plugin.
If plugin call another plugin that not good
## Governace
Check whether the core is work fine or not and how often the core change and check if add another plugin it work or not.