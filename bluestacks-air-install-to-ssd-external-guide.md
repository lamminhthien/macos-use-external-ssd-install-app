# Move BlueStacks Air Data to External USB Drive (macOS)

This guide explains how to move BlueStacks Air application data from your Mac's internal storage to an external USB drive using symbolic links (symlinks).

## About BlueStacks Air

BlueStacks Air is a cloud-based Android emulator that allows you to play mobile games on your Mac. While it's cloud-based, it still stores data locally on your Mac, which can take up significant disk space.

## What is a Symlink?

A symbolic link (symlink) acts like a shortcut. When BlueStacks looks for its data folder on your Mac, it will automatically follow the symlink to find the actual data on your USB drive.

## Prerequisites

- BlueStacks Air installed on macOS
- External USB drive with sufficient space (recommended: USB 3.0 or faster for better performance)
- Basic familiarity with Terminal

## Warning ⚠️

- **Backup your data** before proceeding
- USB drive must be connected whenever you use BlueStacks Air
- USB drive performance may be slower than internal storage
- Make sure the USB drive name stays consistent

## Step-by-Step Instructions

### 1. Close BlueStacks Air Completely

Make sure BlueStacks Air is not running. Quit the application completely.

```bash
# Force quit if needed
killall BlueStacks
```

### 2. Identify Your Paths

**Original BlueStacks Air data location:**
```
/Users/Shared/Library/Application Support/BlueStacks
```

**Your USB drive location** (replace with your actual USB name):
```
/Volumes/YOUR_USB_NAME/Bluestacks Air
```

### 3. Move the Data to USB

Open Terminal and run:

```bash
# Move the entire BlueStacks folder to your USB drive
mv "/Users/Shared/Library/Application Support/BlueStacks" "/Volumes/YOUR_USB_NAME/Bluestacks Air"
```

Replace `YOUR_USB_NAME` with your actual USB drive name (e.g., "Thien 128GB").

### 4. Create the Symlink

Create a symlink that points from the original location to the USB:

```bash
ln -s "/Volumes/YOUR_USB_NAME/Bluestacks Air" "/Users/Shared/Library/Application Support/BlueStacks"
```

### 5. Verify the Symlink

Check that the symlink was created correctly:

```bash
ls -la "/Users/Shared/Library/Application Support/" | grep BlueStacks
```

You should see output like:
```
BlueStacks -> /Volumes/YOUR_USB_NAME/Bluestacks Air
```

### 6. Test BlueStacks Air

Launch BlueStacks Air and verify that everything works correctly.

## Example with Actual Path

If your USB drive is named "Thien 128GB":

```bash
# 1. Move data to USB
mv "/Users/Shared/Library/Application Support/BlueStacks" "/Volumes/Thien 128GB/Bluestacks Air"

# 2. Create symlink
ln -s "/Volumes/Thien 128GB/Bluestacks Air" "/Users/Shared/Library/Application Support/BlueStacks"
```

## Understanding Symlink Direction

**❌ Wrong direction (data stays on Mac):**
```bash
ln -s "/Users/Shared/.../BlueStacks" "/Volumes/USB/Bluestacks Air"
```

**✅ Correct direction (data moves to USB):**
```bash
ln -s "/Volumes/USB/Bluestacks Air" "/Users/Shared/.../BlueStacks"
```

**Rule:** The symlink goes on your Mac, pointing to the actual data on USB.

## Troubleshooting

### BlueStacks won't start
- Verify USB drive is connected and mounted
- Check symlink with: `ls -la "/Users/Shared/Library/Application Support/BlueStacks"`
- Ensure USB drive name hasn't changed

### "No such file or directory" error
- Make sure you moved the folder before creating the symlink
- Verify the USB path is correct (check capitalization and spaces)

### Slow performance
- USB 2.0 drives are significantly slower than internal storage
- Consider using USB 3.0 or faster drives
- SSD-based external drives work best

## Reverting Back to Internal Storage

To move data back to your Mac:

```bash
# 1. Close BlueStacks
# 2. Remove the symlink
rm "/Users/Shared/Library/Application Support/BlueStacks"

# 3. Move data back from USB
mv "/Volumes/YOUR_USB_NAME/Bluestacks Air" "/Users/Shared/Library/Application Support/BlueStacks"
```

## Additional Notes

- The USB drive must be mounted with the same name each time
- If you rename your USB drive, you'll need to recreate the symlink
- This method works for other applications too, not just BlueStacks
- Consider formatting USB as APFS for better macOS compatibility

## License

This guide is provided as-is for educational purposes.

## Contributing

Feel free to submit issues or pull requests if you have improvements or corrections.
