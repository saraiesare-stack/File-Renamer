"""
Advanced File Renamer Script
----------------------------
This script renames all files inside a given folder using:
- Sequential numbering
- Current date stamp

Useful for organizing large collections of files.

Author: SareSaraie
"""

import os
from datetime import datetime


def rename_files(folder_path: str, prefix: str = "file") -> None:
    """
    Rename all files in the specified folder.

    Args:
        folder_path (str): Path to the target folder.
        prefix (str): Prefix for renamed files.
    """

    if not os.path.exists(folder_path):
        print("❌ Folder does not exist.")
        return

    files = os.listdir(folder_path)
    date_str = datetime.now().strftime("%Y%m%d")

    for index, filename in enumerate(files, start=1):
        old_path = os.path.join(folder_path, filename)

        # Skip directories
        if not os.path.isfile(old_path):
            continue

        file_extension = os.path.splitext(filename)[1]
        new_name = f"{prefix}_{index}_{date_str}{file_extension}"
        new_path = os.path.join(folder_path, new_name)

        os.rename(old_path, new_path)

    print("✅ Files renamed successfully.")


if __name__ == "__main__":
    target_folder = "files"  # Change this to your folder path
    rename_files(target_folder)
