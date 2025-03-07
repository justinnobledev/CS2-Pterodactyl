# CS2 on Pterodactyl

Docker image and Pterodactyl egg to prepare for upcoming CS (CS:GO/CS2) updates. The Docker image is based on the Valve provided SteamRT3 Sniper package, with the Pterodactyl egg featuring a few exposed variables such as Beta selection variables and allowing for skipping SteamCMD on launch (i.e, preventing updates). This should allow existing CSGO servers to easily stay on the opt-in CS:GO branch once CS2 releases.

This setup is very similar to the stock Pterodactyl Source server setup, so things should be familiar once imported.

The underlying Docker image is based on Valve's Steam Runtime 3 (Sniper), which should be able to run both CS:GO and CS2 without any issues. The image also can be rebuilt easily as soon as Valve updates their base SteamRT3 image, so we can stay on top of their updates without worrying too much about it. 

## How to use

- Download egg(s) from the `/pterodactyl` directory.
  - `cs2.json`: Egg for CS2
  - `csgo.json`: Egg for CS:GO
- Import into your Pterodactyl nest of choice. [Read here if you need a guide on how to do this.](https://github.com/parkervcp/eggs#how-to-import-an-egg)

## I want to use the Docker image for my own eggs

The Docker image is hosted on the GitHub Container Registry. You can grab it from here: 
```
ghcr.io/1zc/steamrt3-pterodactyl:latest
```

Alternatively, you can find a full list of builds here: https://github.com/1zc/CS2-Pterodactyl/packages

## Frequent Issues

- My CS2 server's public IP address differs from the containers allocated IP, or my CS2 server is crashing due to failing to bind IP
  - Make sure you are using the correct IP address, and then try enabling "Force Outgoing IP" in the egg's configuration in your Pterodactyl Panel admin section.
  - `net_public_adr` doesn't work on CS2 at the time of writing this, so the above is a (hopefully) temporary workaround.
- What operating systems can I run my CS2 server on?
  - At the moment, it appears CS2 will run on the following without issues:
    - Ubuntu 20.04+
    - Debian 11+
    - *If you find any more, please open an issue and I'll add it to this list!*

## General Tips

- Check out the repository's [issue tab](https://github.com/1zc/CS2-Pterodactyl/issues) to look for or discussion solutions to problems you may be facing. 
- Running CS:GO post-CS2 launch will cause the server to constantly spam that it needs an update, you can use the [Cleaner SourceMod extension](https://github.com/accelerator74/Cleaner/tree/master) to get rid of these messages if they're annoying. Edit `addons/sourcemod/configs/cleaner.cfg` and add the following<sup>[#2](https://github.com/1zc/CS2-Pterodactyl/issues/2)</sup>:
  ```
  MasterRequestRestart
  Your server needs to be restarted in order to receive the latest update.
  ```
- If your server on the CS:GO egg keeps trying to restart itself to update (or spamming messages about auto-restarting for updates), remove `-autoupdate` from your server's start-up command.
- Check out the list of available console variables in CS2 on [Valve's Developer Community wiki](https://developer.valvesoftware.com/wiki/List_of_Counter-Strike_2_console_commands_and_variables).
