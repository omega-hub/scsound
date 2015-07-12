## scsound
omegalib sound support based on SuperCollider

**NOTE**: this module is currently working on Windows only. On other operating systems, if you have a local SuperCollider installation, you can very easily adapt `__init.py__` to use it to start the omegalib sound server using the local SuperCollider. Refer to the **How does it Work** section for info on how this module starts and stops the sound server.

### How to Use:
- Install as usual (enable MODULES_scsound in omegalib cmake).
- No need to rebuild omegalib, after cmake configuration you are ready to go!
- To enable sound, add something like this to your configuration file (inside the `config` section):
```
	initCommand = "import scsound; scsound.start()";
	sound:
	{
		soundServerIP = "127.0.0.1";
		soundServerPort = 57120;
                // Do not use the asset cache to manage file transfers: files will be opened locally.
                assetCacheEnabled = false;
	};
```
**NOTE**: the system/desktop-sound.cfg that comes with the omegalib distribution is already configured to play
sound correctly on your local machine (if you ave this module installed).

To run a simple example:
```
> orun scsound/test/welcome.py -c system/desktop-sound.cfg
```

The supercollider server process will start and stop automatically with the application.
A full reference to the sound API can be accessed here: https://github.com/uic-evl/omegalib/wiki/Sound-management

### How does it work
The `scsound.start()` command uses the `olaunch` omegalib function to start a process with the supercollider server. The server is started through a batch file (needed to enter the correct directory before launching).
The scsound module also registers an exit callback (using the python `atexit` module). The exit callback invokes another batch script which shuts down the supercollider processes using the Windows `taskkill` command.
