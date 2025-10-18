# Aikar Flags - Optimized JVM Configuration

## What Are Aikar Flags?

Aikar flags are a set of highly optimized JVM (Java Virtual Machine) parameters specifically tuned for Minecraft servers. They were created by Aikar (a Paper developer) to provide better garbage collection, reduced lag spikes, and improved overall server performance.

## Current Configuration

The default `msh-config.json` now includes Aikar flags optimized for **1GB RAM allocation**:

```json
"StartServerParam": "-Xms1G -Xmx1G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1"
```

## Benefits

✅ **Reduced Lag Spikes** - Better garbage collection scheduling  
✅ **Improved TPS** - Optimized memory management  
✅ **Lower Memory Overhead** - More efficient memory usage  
✅ **Faster Startup** - AlwaysPreTouch pre-allocates memory  
✅ **Better G1GC Tuning** - Specifically optimized for Minecraft's workload  

## Customizing RAM Allocation

### For Different RAM Amounts

Simply change `-Xms` and `-Xmx` to match your server's allocated RAM:

#### 2GB RAM
```
-Xms2G -Xmx2G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1
```

#### 4GB RAM
```
-Xms4G -Xmx4G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1
```

#### 8GB RAM
```
-Xms8G -Xmx8G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1
```

#### 10GB+ RAM (Large Servers)
```
-Xms10G -Xmx10G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1
```

### For Pterodactyl Users

Edit the `SERVER_MEMORY` environment variable in the Pterodactyl panel, and the startup script will automatically set the correct Xms/Xmx values if using the variable approach.

## Flag Breakdown

| Flag | Purpose |
|------|---------|
| `-Xms` / `-Xmx` | Set initial and maximum heap size (should be equal) |
| `-XX:+UseG1GC` | Use G1 Garbage Collector (best for Minecraft) |
| `-XX:+ParallelRefProcEnabled` | Parallel reference processing |
| `-XX:MaxGCPauseMillis=200` | Target max GC pause time of 200ms |
| `-XX:+UnlockExperimentalVMOptions` | Enable experimental JVM options |
| `-XX:+DisableExplicitGC` | Prevent code from forcing GC |
| `-XX:+AlwaysPreTouch` | Pre-touch memory for faster access |
| `-XX:G1NewSizePercent=30` | G1 new generation minimum size |
| `-XX:G1MaxNewSizePercent=40` | G1 new generation maximum size |
| `-XX:G1HeapRegionSize=8M` | G1 heap region size |
| `-XX:G1ReservePercent=20` | G1 reserve memory percentage |
| `-XX:G1HeapWastePercent=5` | G1 heap waste percentage |
| `-XX:G1MixedGCCountTarget=4` | G1 mixed GC count target |
| `-XX:InitiatingHeapOccupancyPercent=15` | When to start marking cycle |
| `-XX:G1MixedGCLiveThresholdPercent=90` | G1 mixed GC live threshold |
| `-XX:G1RSetUpdatingPauseTimePercent=5` | G1 RSet updating pause time |
| `-XX:SurvivorRatio=32` | Ratio of eden to survivor space |
| `-XX:+PerfDisableSharedMem` | Disable shared memory for perf |
| `-XX:MaxTenuringThreshold=1` | Objects move to old gen quickly |

## Compatibility

- **Requires**: Java 8 or newer (Java 17+ recommended)
- **Works with**: Paper, Spigot, Vanilla, Forge, Fabric, etc.
- **Tested on**: Linux, Windows, macOS
- **Best for**: Servers with 1GB+ RAM

## How to Apply

### Method 1: Edit msh-config.json
```bash
nano msh-config.json
# Edit "StartServerParam" under "Commands" section
```

### Method 2: Command Line Flag (Overrides config)
```bash
./msh -msparam "-Xms2G -Xmx2G -XX:+UseG1GC ..."
```

### Method 3: Pterodactyl Egg Variable
The Pterodactyl egg includes a `STARTUP_PARAMS` variable you can customize.

## Important Notes

⚠️ **Always set `-Xms` and `-Xmx` to the same value** - This prevents heap resizing overhead  
⚠️ **Don't allocate all your RAM** - Leave 1-2GB for the OS and MSH  
⚠️ **Java 17+ recommended** - Better performance and newer GC improvements  
⚠️ **Test on your server** - Performance can vary based on mods/plugins  

## Performance Monitoring

Enable resource monitoring in msh-config.json to see the benefits:
```json
"ShowResourceUsage": true,
"ShowInternetUsage": true
```

## References

- [Aikar's Flags Gist](https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/)
- [Paper Optimization Guide](https://paper-chan.moe/paper-optimization/)
- [Oracle G1GC Documentation](https://docs.oracle.com/javase/9/gctuning/garbage-first-garbage-collector-tuning.htm)

## Credits

- **Aikar** - Original flag optimization research
- **Paper Team** - Continued JVM tuning research
- **Community** - Testing and feedback

---

**Note**: These are the default flags included in `msh-config.json` as of v2.5.2-config. You can always customize them based on your server's specific needs!
