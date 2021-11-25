---
layout: page
title: FAQ
parent: Wiki
nav_order: 1
---

# FAQ

### Q: Where can I open my map?
By default, it's your servers public ip-address (e.g. `123.45.67.8`) and the port (`8100`) like this: `http://123.45.67.8:8100/`<br>
*(Make sure you replace `123.45.67.8` with **your** server-ip. The same ip that you are using to connect to your minecraft-server!)*

### Q: I still can't access the website!
Here is a checklist:
- Is the port (`8100` by default) open and forwarded correctly? Or is your firewall blocking incoming connections 
  on the port? If you don't know this **ask your server-host how you can open a second port for BlueMap!**.
- Have you set the correct public ip of your server in the configuration? (E.g. `ip: "123.45.67.8"`)<br>
  **Also try to use the default** `ip` **setting!** *(Have a `#` in front of the line to comment it out)*
  This works on almost all servers!
- Do you get a message saying `Webserver started...` in your server-console/log? If not, look if there are any 
  errors/warnings and check the configuration again.

### Q: I am getting `404 - Not Found` when i open the map
Check your `core.conf` configuration file, did you set `accept-download` to `true`?<br>
If yes, check if your `webroot` settings in `render.conf` and `webserver.conf` are set to the correct (same) folder.

### Q: My map isn't updating!
BlueMap needs to wait until the server saves the world data to disk, so it may take some time for changes to appear 
on the map. Also make sure to click `Update Map` in the menu on the left to make your browser fetch a fresh copy.

### Q: I have black/pink-checkered blocks on my map!
Read this: https://github.com/BlueMap-Minecraft/BlueMap/wiki/Configuring-mods

### Q: My block-textures are messed up when i zoom in on the map!
First, press the `Update Map` button in BlueMap's menu. This updates all tiles from the server and makes sure 
your browser has not cached anything weird.<br>
You can also try to clear your browser-cache completely. *(`F12` -> Network -> [x] Disable cache -> `F5`)*

If that doesn't help you might have changed some bluemap-settings that require a complete re-render of the map:
Just use `/bluemap purge <map-id>` to delete and re-render the entire map. Then clear your browser-cache again,
and it should be fixed :)

### Q: I have a black map / a lot of the map is missing!
- Press the `Update Map` button in BlueMap's menu. This updates all tiles from the server and makes sure your 
  browser has not cached anything weird.
- BlueMap can only render the parts of your world that have already been generated by Minecraft! (E.g., by exploring
  your world or using a plugin to pre-generate an area of your world.)
- Use the command `/bluemap debug block` (in-game). If that is throwing an error, it is likely that you have a mod 
  installed that is not compatible with bluemap. 
  Check the [incompatibilities-list](#known-incompatibilities-with-other-mods) below. 
  If you don't have any mod from the list, please report the error
  [here](https://github.com/BlueMap-Minecraft/BlueMap/issues).
- If nothing else works, you can try to set `ignoreMissingLightData: true` in your 
  map configuration (`render.conf`).<br>
  This will ignore potentially missing light data while rendering, with some drawbacks:
    - Cave-rendering will always be enabled, because it is using the sun-light data to detect the "caves"
    - Everything on the map will be rendered fully lit (sun-light value of 15, looks similar to having night-vision)

### Q: The map (web-app) is really slow (lagging)
Make sure you have **hardware-acceleration enabled** on your browser! 
Use your favorite search engine to learn how to do this :)

### Q: BlueMap does not find my world!
You have to add all your worlds to BlueMap's `render.conf`!<br>
BlueMap has the `world`-world preconfigured. If your world-folder is not called `world` 
(or `world_nether`/`world_the_end` on spigot/paper) then you will need to change the default's in the `render.conf`.

### Q: How can i add SSL (HTTPS) to my map?
BlueMaps integrated webserver does not (and will not) support SSL on its own, 
but you can e.g. [use NGINX to reverse-proxy your map]({{site.baseurl}}/wiki/webserver/NginxProxy.html) 
and add SSL that way.

## Known incompatibilities with other mods
- JustEnoughIDs (jeid)
- NotEnoughIDs
- OpenCubicChunks
- SlimeWorldManager