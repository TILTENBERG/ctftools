import os
import zipfile
import tarfile
import time

def solve_nested_archives_smarter():
    start_file = None
    for f in os.listdir('.'):
        if f.endswith('.zip'):
            start_file = f
            break
    
    if not start_file:
        print("❌ Error: No starting .zip file found in this directory.")
        return

    current_filename = start_file

    while True:
        if not os.path.exists(current_filename):
            print(f"❌ Error: File '{current_filename}' not found. Stopping.")
            break

        print(f"Processing: {current_filename}")
        
        next_filename = None
        is_archive = False

        if zipfile.is_zipfile(current_filename):
            is_archive = True
            print("  Detected type: Zip Archive")
            with zipfile.ZipFile(current_filename, 'r') as zip_ref:
                next_filename = zip_ref.namelist()[0]
                zip_ref.extractall()
                print(f"  ✅ Extracted '{next_filename}'")
        
        elif tarfile.is_tarfile(current_filename):
            is_archive = True
            print("  Detected type: Tar Archive")
            with tarfile.open(current_filename, 'r:*') as tar_ref:
                next_filename = tar_ref.getnames()[0]
                tar_ref.extractall()
                print(f"  ✅ Extracted '{next_filename}'")

        if is_archive:
            print(f"  🗑️ Deleting old archive: {current_filename}")
            os.remove(current_filename)
            current_filename = next_filename
            time.sleep(0.05)
        else:
            print("\n🏁 File is not a recognized zip or tar archive.")
            print(f"Final file reached: {current_filename}")
            print("Inspect this file manually to see what it is.")
            break

if __name__ == "__main__":
    solve_nested_archives_smarter()
