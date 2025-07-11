import sys
import os
import shutil
from datetime import datetime
import argparse

def get_valid_directory(prompt):
    """
    Repeatedly prompt user for a valid directory path.
    
    Args:
        prompt (str): Message to display to user
    
    Returns:
        str: Valid directory path
    """
    while True:
        path = input(prompt).strip()
        
        # Handle user entering empty string
        if not path:
            print("Error: Path cannot be empty. Please try again.")
            continue
            
        # Remove quotes if user included them
        path = path.strip('"\'')
        
        # Convert relative path to absolute path
        path = os.path.abspath(path)
        
        if prompt.lower().startswith('enter source'):
            # For source directory, it must exist
            if not os.path.exists(path):
                print(f"Error: The path '{path}' does not exist. Please enter a valid path.")
                continue
            if not os.path.isdir(path):
                print(f"Error: '{path}' is not a directory. Please enter a valid directory path.")
                continue
        
        return path

def create_backup(source_dir, dest_dir):
    """
    Create backup of files from source directory to destination directory.
    
    Args:
        source_dir (str): Path to source directory
        dest_dir (str): Path to destination directory
    
    Returns:
        tuple: (success_count, error_count)
    """
    # Check if source directory exists
    if not os.path.exists(source_dir):
        raise FileNotFoundError(f"Source directory '{source_dir}' does not exist")
    
    # Check if source is a directory
    if not os.path.isdir(source_dir):
        raise NotADirectoryError(f"'{source_dir}' is not a directory")
    
    # Create destination directory if it doesn't exist
    os.makedirs(dest_dir, exist_ok=True)
    
    success_count = 0
    error_count = 0
    
    # Get list of files in source directory
    try:
        files = os.listdir(source_dir)
    except PermissionError:
        raise PermissionError(f"Permission denied accessing '{source_dir}'")
    
    for filename in files:
        source_file = os.path.join(source_dir, filename)
        
        # Skip if it's a directory
        if os.path.isdir(source_file):
            continue
            
        try:
            # Generate destination file path
            dest_file = os.path.join(dest_dir, filename)
            
            # If file already exists in destination, append timestamp
            if os.path.exists(dest_file):
                # Get file extension
                file_name, file_ext = os.path.splitext(filename)
                # Generate timestamp
                timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
                # Create new filename with timestamp
                new_filename = f"{file_name}_{timestamp}{file_ext}"
                dest_file = os.path.join(dest_dir, new_filename)
            
            # Copy the file
            shutil.copy2(source_file, dest_file)
            print(f"Successfully backed up: {filename}")
            success_count += 1
            
        except PermissionError:
            print(f"Error: Permission denied accessing '{filename}'")
            error_count += 1
        except Exception as e:
            print(f"Error backing up '{filename}': {str(e)}")
            error_count += 1
    
    return success_count, error_count

def main():
    # Set up argument parser
    parser = argparse.ArgumentParser(description='Backup files from source to destination directory')
    parser.add_argument('source', nargs='?', help='Source directory path')
    parser.add_argument('destination', nargs='?', help='Destination directory path')
    
    # Parse arguments
    args = parser.parse_args()
    
    # If arguments weren't provided, ask for them interactively
    source_dir = args.source if args.source else get_valid_directory("Enter source directory path: ")
    dest_dir = args.destination if args.destination else get_valid_directory("Enter destination directory path: ")
    
    try:
        print("\nStarting backup process...")
        print(f"Source directory: {source_dir}")
        print(f"Destination directory: {dest_dir}\n")
        
        # Perform backup
        success_count, error_count = create_backup(source_dir, dest_dir)
        
        # Print summary
        print("\nBackup Summary:")
        print(f"Successfully backed up: {success_count} files")
        if error_count > 0:
            print(f"Failed to backup: {error_count} files")
            sys.exit(1)
            
    except Exception as e:
        print(f"\nError: {str(e)}")
        sys.exit(1)

if __name__ == "__main__":
    main()