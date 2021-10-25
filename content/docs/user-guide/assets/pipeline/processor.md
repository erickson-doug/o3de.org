---
description: ' Use Asset Processor in Open 3D Engine to detect and process new or modified
  asset files. '
title: Using Asset Processor
---

Asset Processor is a utility that runs in the background to detect changes to your asset files. When Asset Processor detects new or updated asset files, it launches the Resource Compiler, processes the assets, and then places them in the cache. Asset Processor then notifies all running game or tool instances that the assets are updated. The game can then reload the updated assets.

As part of Asset Processing, the Asset Processor generates and stores product and source dependencies . In this context, a dependency defines how a one product or source asset depends on another asset. A given asset may have 0 or more dependencies, and these dependencies are used by features such as the [Asset Bundler](/docs/user-guide/packaging/asset-bundler) in order to determine which assets must be included when you bundle your game for release.

Asset Processor enables games to run on other platforms without deploying assets to that platform. Instead, the assets are accessed from the asset cache on a connected Windows or macOS system. With Asset Processor, you can also run games that use someone else's assets.

By proxying requests through itself, Asset Processor communicates with an iOS or Android shader compiler server through a USB cable on iOS and Android.

In Windows, Asset Processor starts automatically if you run O3DE Editor with automatically maintained connections. Asset Processor also restarts automatically if you modify any of the data files that it needs to operate or if you retrieve a new version.

{{< note >}}
Symbolic links are not supported when using Asset Processor in macOS. To ensure that Asset Processor works properly in macOS, follow these guidelines:

+ Do not use a symbolic link for your cache directory when you store compiled assets in a central location.
+ Do not store your source project assets in a symbolic link directory.
+ Use a unique cache directory. Do not share the cache directory with a Windows system that is also running Asset Processor.
{{< /note >}}

 You can open the Asset Processor options from the notification area on the taskbar.

![Right-click the Asset Processor icon in your notification area on the taskbar, and then choose Show.](/images/user-guide/assets/pipeline/asset-pipeline-processor-options.png)

You don't need to close Asset Processor when you get the latest updates from source control. You can start O3DE Editor while Asset Processor is still processing your assets.

However, if you aren't using the game or O3DE Editor, you can exit Asset Processor by right-clicking its icon in the notification area on the Windows taskbar or the macOS menu bar.

Asset Processor can also serve files directly to devices, avoiding copying assets aren't required to be present on the game device. This is called virtual file system (VFS) and is required for live reloading to work on those platforms.

## Modifying the Asset Processor Configuration Using a Settings Registry File

Modify the engine settings registry file for the Asset Processor in `Registry/AssetProcessorPlatformConfig.setreg` to perform the following tasks:
+ Add new file types for Asset Processor to feed to the Resource Compiler, copy into the cache, or update existing file type rules.
+ Update the ignore list.
+ Specify which platforms are currently enabled. The default value is the host platform that Asset Processor runs on. Asset Processor automatically builds assets for the host platform. For example, if Asset Processor is running on Windows, Asset Processor builds Windows assets even if **pc** is not enabled in the `.setreg` file. If Asset Processor is running on macOS, Asset Processor builds macOS assets even if **osx\_gl** is not enabled in the `.setreg` file. To build assets for other platforms, update the `.setreg` file and specify the platforms that you want.
+ Add additional folders for Asset Processor to watch. For example, you can specify folders such as shared particle libraries and associated textures between projects.
+ Specify which files trigger related files to be rebuilt. This is called metafile fingerprinting.

To add game-specific overrides, you can add a file named `AssetProcessorGamePlatformConfig.setreg` to your game's `Registry` directory. This file is read after the root configuration file and can have additional game-specific settings for the ignore list, platforms, and file types.

## Using the Asset Processor Batch Program 

The `AssetProcessorBatch.exe` application compiles all assets for the current project and enabled platforms. If the process succeeds without errors, it exits with a `0` code. You can use the Asset Processor Batch program as part of your build system for automation.

The `AssetProcessorBatch.exe` file accepts the following command line parameters for overriding the default behavior:
+ `/platforms=comma separated list`
+ `/gamefolder=name of game folder`

Example:

`AssetProcessorBatch.exe /platforms=pc,ios /gamefolder=SamplesProject`
