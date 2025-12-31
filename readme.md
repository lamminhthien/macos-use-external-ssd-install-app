# Move macOS Application Data to External SSD

A simple guide to free up space on your Mac by moving large application folders to an external SSD using symbolic links (symlinks).

## What is a Symlink?

A symbolic link (symlink) is like a shortcut. When an app looks for its data folder on your Mac, it automatically follows the symlink to find the actual data on your external SSD.

## ⚠️ Important Rules

1. **MUST move or delete the old folder** - Don't keep both the original and the copy
2. **The symlink replaces the original folder** on your Mac
3. **External SSD must be connected** when using these apps
4. **Backup your data** before starting

## How It Works

```
Mac Internal Storage          External SSD
[Symlink] ----------------->  [Real Data]
```

Your Mac has a "pointer" that redirects to the real data on the SSD.

## Basic Steps (For Any App)

### 1. Close the Application Completely

Quit the app you want to move. Force quit if needed:

```bash
# Example for BlueStacks
killall BlueStacks
```

### 2. Move the Data Folder to SSD

**⚠️ IMPORTANT: This moves (not copies) the folder. The original location will be empty.**

```bash
mv "/path/to/original/folder" "/Volumes/YOUR_SSD_NAME/FolderName"
```

### 3. Create Symlink

Create a symlink pointing from the original location to the SSD:

```bash
ln -s "/Volumes/YOUR_SSD_NAME/FolderName" "/path/to/original/folder"
```

### 4. Verify

Check the symlink was created:

```bash
ls -la "/path/to/original/folder"
```

You should see: `folder -> /Volumes/YOUR_SSD_NAME/FolderName`

---

## Common Applications to Move

Replace `YOUR_SSD_NAME` with your actual SSD name (e.g., "External_SSD").

### 🎮 BlueStacks Air (Android Emulator)

**Size:** 5-20 GB

```bash
# Close BlueStacks first
killall BlueStacks

# Move data
mv "/Users/Shared/Library/Application Support/BlueStacks" "/Volumes/YOUR_SSD_NAME/BlueStacks"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/BlueStacks" "/Users/Shared/Library/Application Support/BlueStacks"
```

---

### 📱 Android Studio Development

#### Android SDK & AVD (~20-50 GB)

```bash
# Move Android folder
mv ~/.android "/Volumes/YOUR_SSD_NAME/android"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/android" ~/.android
```

#### Gradle Cache (~5-20 GB)

```bash
# Move Gradle folder
mv ~/.gradle "/Volumes/YOUR_SSD_NAME/gradle"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/gradle" ~/.gradle
```

---

### 📦 Node.js Development

#### NVM (Node Version Manager) (~2-10 GB)

```bash
# Move NVM folder
mv ~/.nvm "/Volumes/YOUR_SSD_NAME/nvm"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/nvm" ~/.nvm
```

#### NPM Cache (~1-5 GB)

```bash
# Move NPM cache
mv ~/.npm "/Volumes/YOUR_SSD_NAME/npm-cache"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/npm-cache" ~/.npm
```

#### Yarn Cache (~1-5 GB)

```bash
# Move Yarn cache
mv ~/Library/Caches/Yarn "/Volumes/YOUR_SSD_NAME/yarn-cache"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/yarn-cache" ~/Library/Caches/Yarn
```

---

### 🍎 Xcode Development

#### Xcode Derived Data (~10-50 GB)

```bash
# Move Derived Data
mv ~/Library/Developer/Xcode/DerivedData "/Volumes/YOUR_SSD_NAME/Xcode-DerivedData"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/Xcode-DerivedData" ~/Library/Developer/Xcode/DerivedData
```

#### Xcode Archives (~5-20 GB)

```bash
# Move Archives
mv ~/Library/Developer/Xcode/Archives "/Volumes/YOUR_SSD_NAME/Xcode-Archives"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/Xcode-Archives" ~/Library/Developer/Xcode/Archives
```

#### Xcode Device Support (~5-15 GB)

```bash
# Move Device Support files
mv ~/Library/Developer/Xcode/iOS\ DeviceSupport "/Volumes/YOUR_SSD_NAME/Xcode-DeviceSupport"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/Xcode-DeviceSupport" ~/Library/Developer/Xcode/iOS\ DeviceSupport
```

#### CocoaPods Cache (~1-3 GB)

```bash
# Move CocoaPods cache
mv ~/Library/Caches/CocoaPods "/Volumes/YOUR_SSD_NAME/CocoaPods-cache"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/CocoaPods-cache" ~/Library/Caches/CocoaPods
```

---

### 💎 Ruby Development

#### RubyGems (~1-5 GB)

```bash
# Move Gems
mv ~/.gem "/Volumes/YOUR_SSD_NAME/gem"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/gem" ~/.gem
```

---

### 🐳 Docker

#### Docker Data (~10-100 GB)

```bash
# Move Docker data
mv ~/Library/Containers/com.docker.docker "/Volumes/YOUR_SSD_NAME/Docker"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/Docker" ~/Library/Containers/com.docker.docker
```

---

### 🎵 Other Large Applications

#### Spotify Cache (~5-10 GB)

```bash
# Move Spotify cache
mv ~/Library/Caches/com.spotify.client "/Volumes/YOUR_SSD_NAME/Spotify-cache"

# Create symlink
ln -s "/Volumes/YOUR_SSD_NAME/Spotify-cache" ~/Library/Caches/com.spotify.client
```

#### Homebrew (~5-20 GB)

```bash
# Move Homebrew
mv /usr/local/Cellar "/Volumes/YOUR_SSD_NAME/Homebrew-Cellar"

# Create symlink
sudo ln -s "/Volumes/YOUR_SSD_NAME/Homebrew-Cellar" /usr/local/Cellar
```

---

## Quick Reference Table

| Application | Path to Move | Typical Size |
|------------|--------------|--------------|
| BlueStacks | `/Users/Shared/Library/Application Support/BlueStacks` | 5-20 GB |
| Android SDK | `~/.android` | 20-50 GB |
| Gradle | `~/.gradle` | 5-20 GB |
| NVM | `~/.nvm` | 2-10 GB |
| NPM Cache | `~/.npm` | 1-5 GB |
| Yarn Cache | `~/Library/Caches/Yarn` | 1-5 GB |
| Xcode Derived Data | `~/Library/Developer/Xcode/DerivedData` | 10-50 GB |
| Xcode Archives | `~/Library/Developer/Xcode/Archives` | 5-20 GB |
| Xcode Device Support | `~/Library/Developer/Xcode/iOS DeviceSupport` | 5-15 GB |
| CocoaPods Cache | `~/Library/Caches/CocoaPods` | 1-3 GB |
| RubyGems | `~/.gem` | 1-5 GB |
| Docker | `~/Library/Containers/com.docker.docker` | 10-100 GB |

---

## Troubleshooting

### ❌ "File exists" error when creating symlink

**Problem:** Original folder still exists

**Solution:** Delete or move it first

```bash
# Remove the old folder (make sure data is on SSD first!)
rm -rf "/path/to/original/folder"

# Then create symlink
ln -s "/Volumes/YOUR_SSD_NAME/FolderName" "/path/to/original/folder"
```

### ❌ "No such file or directory" error

**Problem:** Wrong path or SSD not connected

**Solution:** 
- Check SSD is mounted: `ls /Volumes/`
- Verify folder exists on SSD: `ls /Volumes/YOUR_SSD_NAME/`

### ❌ App won't start

**Problem:** SSD not connected or symlink broken

**Solution:**
- Connect your SSD
- Check symlink: `ls -la /path/to/symlink`

---

## Reverting Back to Internal Storage

To move data back to your Mac:

```bash
# 1. Close the application
# 2. Remove the symlink (NOT the folder on SSD!)
rm "/path/to/symlink"

# 3. Move data back from SSD
mv "/Volumes/YOUR_SSD_NAME/FolderName" "/path/to/original/folder"
```

---

## Pro Tips

✅ **Use APFS formatted SSD** for best macOS compatibility  
✅ **Use USB 3.0+ or Thunderbolt** for fast performance  
✅ **Name your SSD without spaces** (easier for Terminal commands)  
✅ **Keep SSD connected** when using moved apps  
✅ **Backup important data** before moving  

---

## Why Move These Folders?

- **Save 50-200+ GB** on your Mac's internal storage
- **Keep frequently used apps** on internal storage for speed
- **Move development caches** that rebuild easily
- **Free up space** for system updates and new apps

---

## License

This guide is provided as-is for educational purposes.

## Contributing

Feel free to submit issues or pull requests with improvements or additional app suggestions!
