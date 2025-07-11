# Backup-Script-with-Timestamp

### Description
This script facilitates the backup of files from a specified source directory to a destination directory. If a file with the same name exists in the destination directory, it appends a timestamp to the filename to avoid overwriting. It is useful for maintaining backups with unique file versions.

### Features
- **Interactive Directory Input**: Prompts the user for valid source and destination directories if not provided as command-line arguments.
- **File Versioning**: Automatically appends a timestamp to duplicate files in the destination directory.
- **Error Handling**: Skips directories in the source, handles permissions errors gracefully, and logs failed backup attempts.
- **Command-Line Arguments**: Supports specifying the source and destination directories via command-line arguments.

### Prerequisites
- Python 3.6 or higher installed on your system.
- Basic knowledge of navigating directories and running Python scripts.

### Requirements
- `shutil` (Standard library module for file operations)
- `os` (Standard library module for directory handling)
- `argparse` (Standard library module for parsing command-line arguments)

### Using the Program

#### 1. **Run the Script**
   You can execute the script via the command line:
   ```bash
   python Backup Script with Timestamp.py [source_directory] [destination_directory]
   ```
   Or, run without arguments for interactive mode.

#### 2. **Interactive Mode**
   If no arguments are provided, the script will prompt:
   ```
   Enter source directory path:
   Enter destination directory path:
   ```

#### 3. **Example Command-Line Input**
   ```bash
   python Backup Script with Timestamp.py /path/to/source /path/to/destination
   ```

#### 4. **Sample Input and Outputs**

**Input:**
- Source Directory: `/user/documents/source/`
- Destination Directory: `/user/documents/destination/`
- Files in Source:
  - `example.txt`
  - `image.png`

**Output:**
```
Starting backup process...
Source directory: /user/documents/source/
Destination directory: /user/documents/destination/

Successfully backed up: example.txt
Successfully backed up: image.png

Backup Summary:
Successfully backed up: 2 files
```

**Scenario with Duplicate Files:**
- Source File: `example.txt`
- Destination already contains: `example.txt`

**Output:**
```
Successfully backed up: example.txt (Renamed to: example_20241123_121530.txt)
```

#### Error Scenarios:
- If the source directory is invalid:
  ```
  Error: The path '/invalid/path/' does not exist. Please enter a valid path.
  ```
- If a file in the source directory cannot be accessed:
  ```
  Error: Permission denied accessing 'restricted_file.txt'
  ```

### Notes
- The timestamp format is `YYYYMMDD_HHMMSS`.
- The script skips subdirectories in the source directory during the backup process.

### License
This script is open-source and can be used and modified freely for personal and educational purposes.
