## scsound
omegalib sound support based on SuperCollider

**NOTE**: this module is currently Windows only.

### How to Use:
- Install as usual (enable MODULES_scsound in omegalib cmake).
- No need to rebuild omegalib, after cmake configuration you are ready to go!
- To enable sound, add something like this to your configuration file:
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
