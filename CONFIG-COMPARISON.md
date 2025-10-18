# msh-config.json Comparison

## ⚠️ Important Differences Found!

The gist config (used in Pterodactyl egg) is **OUTDATED** and missing critical fields.

### Missing Fields in Gist Config

#### 1. Query Support (NEW)
```json
// REPO (✅ Current)
"MshPortQuery": 25555,
"EnableQuery": true,

// GIST (❌ Missing)
// These fields don't exist!
```

#### 2. Advanced Features (NEW)
```json
// REPO (✅ Current)
"WhitelistImport": false,
"ShowResourceUsage": false,
"ShowInternetUsage": false,
"SuspendRefresh": -1,

// GIST (❌ Missing)
// Only has "AllowSuspend" (old name)
```

#### 3. Port Naming (BREAKING CHANGE)
```json
// REPO (✅ Current)
"MshPort": 25555,
"MshPortQuery": 25555,

// GIST (❌ Old name)
"ListenPort": 25555,  // Renamed to MshPort!
```

#### 4. Suspend Configuration
```json
// REPO (✅ Current)
"SuspendAllow": false,
"SuspendRefresh": -1,

// GIST (❌ Old name)
"AllowSuspend": false,  // Renamed to SuspendAllow!
// SuspendRefresh is missing!
```

#### 5. Server Info
```json
// REPO (✅ Current)
"Folder": "{path/to/server/folder}",  // Placeholder
"FileName": "{server.jar}",           // Placeholder
"Version": "1.19.2",
"Protocol": 760,

// GIST (❌ Specific values)
"Folder": "./",
"FileName": "server.jar",
"Version": "1.17.1",  // Outdated!
"Protocol": 756,      // Old protocol!
```

## 🔍 Side-by-Side Comparison

### Repo Version (Current - v2.5.2)
```json
{
  "Server": {
    "Folder": "{path/to/server/folder}",
    "FileName": "{server.jar}",
    "Version": "1.19.2",
    "Protocol": 760
  },
  "Commands": {
    "StartServer": "java <Commands.StartServerParam> -jar <Server.FileName> nogui",
    "StartServerParam": "-Xmx1024M -Xms1024M",
    "StopServer": "stop",
    "StopServerAllowKill": 10
  },
  "Msh": {
    "Debug": 1,
    "ID": "",
    "MshPort": 25555,              ← NEW
    "MshPortQuery": 25555,         ← NEW
    "EnableQuery": true,            ← NEW
    "TimeBeforeStoppingEmptyServer": 30,
    "SuspendAllow": false,          ← RENAMED
    "SuspendRefresh": -1,           ← NEW
    "InfoHibernation": "...",
    "InfoStarting": "...",
    "NotifyUpdate": true,
    "NotifyMessage": true,
    "Whitelist": [],
    "WhitelistImport": false,       ← NEW
    "ShowResourceUsage": false,     ← NEW
    "ShowInternetUsage": false      ← NEW
  }
}
```

### Gist Version (Outdated)
```json
{
  "Server": {
    "Folder": "./",
    "FileName": "server.jar",
    "Version": "1.17.1",           ← OLD VERSION
    "Protocol": 756                 ← OLD PROTOCOL
  },
  "Commands": {
    "StartServer": "java <Commands.StartServerParam> -jar <Server.FileName> nogui",
    "StartServerParam": "-Xmx1024M -Xms1024M",
    "StopServer": "stop",
    "StopServerAllowKill": 10
  },
  "Msh": {
    "ID": "52fdfc0721feefe75af65af163f82654f163f",
    "Debug": 1,
    "AllowSuspend": false,          ← OLD NAME (should be SuspendAllow)
    "InfoHibernation": "...",
    "InfoStarting": "...",
    "NotifyUpdate": true,
    "NotifyMessage": true,
    "ListenPort": 25555,            ← OLD NAME (should be MshPort)
    "TimeBeforeStoppingEmptyServer": 30,
    "Whitelist": []
    // Missing: MshPortQuery, EnableQuery, SuspendRefresh, 
    //          WhitelistImport, ShowResourceUsage, ShowInternetUsage
  }
}
```

## ⚠️ Impact on Pterodactyl Egg

The egg currently downloads the **outdated gist config**, which means:

1. **Missing Query Support** - Server query won't work properly
2. **Old Field Names** - May cause compatibility issues
3. **Missing Features** - WhitelistImport, ShowResourceUsage, ShowInternetUsage won't be available
4. **Outdated MC Version** - Shows 1.17.1 instead of 1.19.2

## 🔧 Recommendation

**UPDATE THE EGG** to use the repo's config file:

### Option 1: Use Raw GitHub URL
```bash
curl -o msh-config.json https://raw.githubusercontent.com/Kartvya69/minecraft-server-hibernation/main/msh-config.json
```

### Option 2: Host in Releases
Add `msh-config.json` to the GitHub release and download from there.

### Option 3: Inline in Installation Script
Embed the config directly in the egg's installation script.

## Priority
**HIGH** - The gist config is incompatible with v2.5.2 and missing critical features!
