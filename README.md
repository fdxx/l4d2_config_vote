## About
Generate a vote menu from a configuration file and vote it.  
  
## Require
- L4D2 dedicated server  
- SourceMod 1.11  
- [left4dhooks](https://github.com/SilvDev/Left4DHooks)  
- [l4d2_nativevote](https://github.com/fdxx/l4d2_nativevote)  
- [l4d2_source_keyvalues](https://github.com/fdxx/l4d2_source_keyvalues)  
  
## Cmd and Cvar
- `l4d2_config_vote_path`: Console Variables, Menu vote config file path.  
- `l4d2_config_vote_menucustomflags`: Console Variables, Menu custom rules of showing.  
- `l4d2_config_vote_adminteamflags`: Console Variables, Admin bypass `*TeamFlags`.  
- `l4d2_config_vote_printmsg`: Console Variables, Whether print hint message to clients.  
- `l4d2_config_vote_passmode`: Console Variables, Method of judging vote pass. 0=Vote Yes count > Vote No count. 1=Vote Yes count > Half of players count.  
- `l4d2_config_vote_icon_selected`: Console Variables, Selected Icon (Default: `[√]`).  
- `l4d2_config_vote_icon_unselected`: Console Variables, Unselected Icon (Default: `[  ]`).  
- `sm_votecfg_reload`: Console Commands (admin), Reload config file.  
- `sm_v`: Console Commands, Open vote menu.  
- `sm_vt`: Console Commands, Open vote menu.  
- `sm_votes`: Console Commands, Open vote menu.  
  
## Config file
  
### Type
- `ServerCommand`：Execute server command or admin command after vote is passed.  
- `ClientCommand`：Execute client command after the vote is passed.  
- `ExternalVote`：Call vote command provided by other plugin after menu selection. Valid item for this type：**MenuTeamFlags**, **Command**.  
- `CheatCommand`：Execute server cheat command after vote is passed.  
  
### SelectType (Optional)
If this property is set on one node, then all of it's first level sub nodes will show a selected icon.  
- `Single`：If one config's vote is passed, this node's icon will be set to selected, and all the other same level nodes' icon will be set to unselected.  
- `Multiple`：If one config's vote is passed, this node's icon will be set to it's opposite.  
- `CvarTracking`：Whether showing the selected icon depends on a specified cvar value.  
- `PluginTracking`：Whether showing the selected icon depends on whether a specified plugin is loaded.  
  
### Selected (Optional)
This property is valid only when **parent level** node's SelectType is specified to `Single` or `Multiple`.  
Marking this node as default selected.  
  
### CvarName (Optional)
This property is valid only when **this level** node's SelectType is specified to `CvarTracking`.  
Specifying the cvar name to track.  
  
### CvarType (Optional)
This property is valid only when **this level** node's SelectType is specified to `CvarTracking`.  
Specifying the cvar value datatype.  
- `int`：Indicate the cvar value is a int type.  
- `float`：Indicate the cvar value is a float type.  
- `string`：Indicate the cvar value is a string type.  
  
### CvarMatch (Optional)
This property is valid only when **parent level** node's SelectType is specified to `CvarTracking`, and **parent level** node's CvarName and CvarType are specified correctly.  
Specifying the voting config value, which matches the specified cvar value, used to show a selected icon.  
  
### PluginMatch (Optional)
This property is valid only when **parent level** node's SelectType is specified to `PluginTracking`.  
Specifying the voting config to load/unload the specified plugin, which matches the specified plugin name, used to show a selected icon.  
  
### MenuCustomFlags (Optional)
Whether clients can see the menu and initiate a vote, based on custom rules. default value: "&lt;Empty String&gt;" (no limits).  
#### Description
The value of `MenuCustomFlags` in the config menu can be set to a comma separated string. For example: "custom1", or "custom1,custom2".  
The value of the plugin cvar `l4d2_config_vote_menucustomflags` can also be set to a comma separated string. For example: "custom1", or "custom1,custom2".  
**If the `MenuCustomFlags` value is "&lt;Empty String&gt; (Not Configured)", then there will be no limits.**  
**If the `MenuCustomFlags` value is configured, then only if the `MenuCustomFlags` and the `l4d2_config_vote_menucustomflags` have some elements in common (the intersection of the `MenuCustomFlags` and the `l4d2_config_vote_menucustomflags` is not empty), this config in the menu can be shown to clients.**  
> Example:  
>     1. `MenuCustomFlags`: "(Not Configured)", no matter what the cvar `l4d2_config_vote_menucustomflags` value is. =&gt; Clients **can see** this vote config in menu.  
>     2. `MenuCustomFlags`: "1", `l4d2_config_vote_menucustomflags`: "1". =&gt; Clients **can see** this vote config in menu.  
>     3. `MenuCustomFlags`: "2", `l4d2_config_vote_menucustomflags`: "1". =&gt; Clients **can not see** this vote config in menu.  
>     4. `MenuCustomFlags`: "1,2", `l4d2_config_vote_menucustomflags`: "1". =&gt; Clients **can see** this vote config in menu.  
>     5. `MenuCustomFlags`: "1,2", `l4d2_config_vote_menucustomflags`: "3". =&gt; Clients **can not see** this vote config in menu.  
>     6. `MenuCustomFlags`: "1", `l4d2_config_vote_menucustomflags`: "1,2". =&gt; Clients **can see** this vote config in menu.  
>     7. `MenuCustomFlags`: "3", `l4d2_config_vote_menucustomflags`: "1,2". =&gt; Clients **can not see** this vote config in menu.  
>     8. `MenuCustomFlags`: "1,2", `l4d2_config_vote_menucustomflags`: "2,3". =&gt; Clients **can see** this vote config in menu.  
  
### MenuModeFlags (Optional)
Whether clients can see the menu and initiate a vote in these gamemodes (based on). coop=1, realism=2, versus=4, survival=8, scavenge=16, default value: 31 (all gamemodes).  
*Note: Mutations are also based on these fundamental gamemodes.*  
  
### MenuTeamFlags (Optional)
Which clients can see the menu and initiate a vote. spectator=2, survivors=4, infected=8, default value: 14 (all teams).  
  
### VoteTeamFlags (Optional)
Which clients can vote. spectator=2, survivors=4, infected=8, default value: 14 (all teams).  
  
### AdminOneVotePassed (Optional)
Whether to enable admin one vote to passed. default value: 1 (enable).  
  
### AdminOneVoteAgainst (Optional)
Whether to enable admin one vote to against. default value: 1 (enable).  
  
### Description
Info displayed after initiating a vote.  
  
### Command
Command executed after the vote is passed.  
