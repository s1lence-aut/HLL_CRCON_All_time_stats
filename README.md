# HLL_CRCON_All_time_stats

A plugin for HLL CRCON (see : https://github.com/MarechJ/hll_rcon_tool)
that does different things on chat commands :  
- `!me` displays statistic data about the player ;
- `!r` offers a "fast redeployment" option, avoiding the 10 secs penalty (autopunish)

![375490122-d8c7be50-aa6e-4949-b789-c327cacb2a1a](https://github.com/user-attachments/assets/4e9105d9-f87b-40e9-a489-da74cbb8f267)

## Install
- Create `custom_tools` folder in CRCON's root (`/root/hll_rcon_tool/`) ;
- Copy `hooks_custom_chatcommands.py` in `/root/hll_rcon_tool/custom_tools/` ;
- Copy `restart.sh` in CRCON's root (`/root/hll_rcon_tool/`) ;
- Edit `/root/hll_rcon_tool/hooks.py` and add these lines:
  - in the import part, on top of the file
    ```python
    import custom_tools.hooks_custom_chatcommands as hooks_custom_chatcommands
    ```
  - At the very end of the file
    ```python
    @on_chat
    def commands_onchat(rcon: Rcon, struct_log: StructuredLogLineWithMetaData):
        hooks_custom_chatcommands.chat_commands(rcon, struct_log)
    ```

## Config
- Edit `/root/hll_rcon_tool/custom_tools/hooks_custom_chatcommands.py` and set the parameters to your needs ;
- Restart CRCON :
  ```shell
  cd /root/hll_rcon_tool
  sh ./restart.sh
  ```

## Limitations
⚠️ Any change to these files :
- `/root/hll_rcon_tool/custom_tools/hooks_custom_chatcommands.py` ;
- `/root/hll_rcon_tool/hooks.py`  
...will need a CRCON restart (using `restart.sh` script) to be taken in account.

⚠️ This plugin requires a modification of the `/root/hll_rcon_tool/hooks.py` file, which originates from the official CRCON depot.  
If any CRCON upgrade implies updating this file, the usual upgrade procedure, as given in official CRCON instructions, will **FAIL**.  
To successfully upgrade your CRCON, you'll have to revert the changes back, then reinstall this plugin.  
To revert to the original file :  
```shell
cd /root/hll_rcon_tool
git restore rcon/hooks.py
```
