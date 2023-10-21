## About
Generate a vote menu from a configuration file and vote it.

## Require
- L4D2 dedicated server
- SourceMod 1.11
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
