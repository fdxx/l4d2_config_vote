## About
Generate a vote menu from a configuration file and vote it.

## Require
- L4D2 dedicated server
- SourceMod 1.11
- [left4dhooks](https://github.com/SilvDev/Left4DHooks)
- [l4d2_nativevote](https://github.com/fdxx/l4d2_nativevote)
- [l4d2_source_keyvalues](https://github.com/fdxx/l4d2_source_keyvalues)

## Cmd and Cvar
- `l4d2_config_vote_adminteamflags`: Console Variables, Admin bypass `*TeamFlags`.
- `sm_votecfg_reload`: Console Commands (admin), Reload config file.
- `sm_votes`: Console Commands, Open vote menu.

## Config file

### Type
- `ServerCommand`：Execute server command or admin command after vote is passed.
- `ClientCommand`：Execute client command after the vote is passed.
- `ExternalVote`：Call vote command provided by other plugin after menu selection. Valid item for this type：**MenuTeamFlags**, **Command**.
- `CheatCommand`：Execute server cheat command after vote is passed.

### MenuCustomFlags (Optional)
Whether clients can see the menu and initiate a vote, based on custom rules. default value: "\<Empty String\>" (no limits).
#### Description:
The value of `MenuCustomFlags` in the config menu can be set to a comma separated string. For example: "custom1", or "custom1,custom2".
The value of the plugin cvar `l4d2_config_vote_menucustomflags` can also be set to a comma separated string. For example: "custom1", or "custom1,custom2".
**If the `MenuCustomFlags` value is "<Empty String> (Not Configured)", then there will be no limits.**
**If the `MenuCustomFlags` value is configured, then only if the `MenuCustomFlags` and the `l4d2_config_vote_menucustomflags` have some elements in common (the intersection of the `MenuCustomFlags` the `l4d2_config_vote_menucustomflags` is not empty), this config in the menu can be shown to clients.**
> Example:
>     1. `MenuCustomFlags`: "<Empty String> (Not Configured)", no matter what the cvar `l4d2_config_vote_menucustomflags` value is. ==> Clients **can see** this vote config in the menu.
>     2. `MenuCustomFlags`: "1", `l4d2_config_vote_menucustomflags`: "1". ==> Clients **can see** this vote config in the menu.
>     3. `MenuCustomFlags`: "2", `l4d2_config_vote_menucustomflags`: "1". ==> Clients **can not see** this vote config in the menu.
>     4. `MenuCustomFlags`: "1", `l4d2_config_vote_menucustomflags`: "1,2". ==> Clients **can see** this vote config in the menu.
>     5. `MenuCustomFlags`: "2", `l4d2_config_vote_menucustomflags`: "1,2". ==> Clients **can see** this vote config in the menu.
>     6. `MenuCustomFlags`: "1,2", `l4d2_config_vote_menucustomflags`: "1". ==> Clients **can see** this vote config in the menu.
>     7. `MenuCustomFlags`: "1,2", `l4d2_config_vote_menucustomflags`: "2". ==> Clients **can see** this vote config in the menu.
>     8. `MenuCustomFlags`: "1,2", `l4d2_config_vote_menucustomflags`: "1,2". ==> Clients **can see** this vote config in the menu.

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
