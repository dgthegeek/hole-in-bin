# Virtual Address to File Offset Converter

This helps you understand and convert between virtual addresses (as seen in disassembly) and file offsets (as seen in hex editors) for binary files, particularly ELF executables.

## Background

When working with binary files, especially during reverse engineering or debugging, you'll often encounter two types of addresses:

1. **Virtual Addresses**: These are the addresses where instructions or data will be loaded in memory when the program runs. Tools like `objdump` typically show these addresses.

2. **File Offsets**: These represent the actual position of bytes within the file itself. Hex editors or tools like `xxd` show these offsets.

## The Difference

The main difference comes from how the operating system loads the executable into memory:

- Virtual Address = Base Address + File Offset

The base address is where the first byte of the file will be loaded into memory. For 32-bit ELF executables on x86 systems, this is often `0x08048000`.

## How to Find the Base Address

You can use the `readelf` command to find the base address:

```bash
readelf -l your_binary | grep LOAD
```

Look for the first LOAD segment. The address in the "VirtAddr" column is typically the base address.


## Why This Matters

Understanding the relationship between virtual addresses and file offsets is crucial for:
- Accurately locating specific instructions or data in a binary file
- Correlating information between different analysis tools
- Patching binaries
- Debugging and reverse engineering

By mastering this concept, you'll be able to navigate between different views of a binary with ease, enhancing your ability to analyze and modify executable files.