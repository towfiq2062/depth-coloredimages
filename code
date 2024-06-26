#Colorizing txt 
#%%pip3 install opencv-python
import cv2
import numpy as np
import os
import shutil

# Source directory containing subdirectories with depth files
src_directory = "/common/"  # Update this path
out_root_directory = "/common/"  # Update this path
#

# Define the structuring element
SE = cv2.getStructuringElement(cv2.MORPH_RECT, (2, 2))

# Create a log file to track processed directories
log_file_path = os.path.join(out_root_directory, 'processed_directories.txt')
with open(log_file_path, 'w') as log_file:
    log_file.write("Processed Directories:\n")

# Walk through all subdirectories and files in the source directory
for root, _, files in os.walk(src_directory):
    for filename in files:
        if filename.endswith('.txt'):
            # Form the output subdirectory path based on the relative path in the source directory
            relative_subdir = os.path.relpath(root, src_directory)
            output_subdir = os.path.join(out_root_directory, relative_subdir)

            # Create the corresponding subdirectory in the output directory if it doesn't exist
            os.makedirs(output_subdir, exist_ok=True)

            # Form the output file path
            filename_out = os.path.splitext(filename)[0] + '.png'
            output_file_path = os.path.join(output_subdir, filename_out)

            # Check if the output file already exists, if yes, skip processing
            if os.path.exists(output_file_path):
                print(f"Skipping {filename_out} (already exists)")
                continue

            # Load depth data from file
            depth_data = np.loadtxt(os.path.join(root, filename), delimiter=',')

            # Apply thresholding to focus on a specific depth range (optional)
            depth_data[np.logical_or(depth_data < 1500, depth_data > 2700)] = 0

            # Apply thresholding to focus on a specific depth range
            depth_normalized = 1 - np.clip((depth_data - 1500) / (2700 - 1500), 0, 1)

            # Apply a color map to the normalized depth datade
            colorized_depth = cv2.applyColorMap((depth_normalized * 255).astype(np.uint8), cv2.COLORMAP_JET)

            # Define the crop coordinates (adjust as needed)
            xPos = [50, 70, 500, 500]  # down down right up
            yPos = [50, 450, 450, 50]

            # Crop the colorized image
            img_cropped = colorized_depth[min(yPos):max(yPos), min(xPos):max(xPos)]

            # Save the cropped colorized image
            cv2.imwrite(output_file_path, img_cropped)
            print(f"Processed {filename_out}")

    # Log the processed directory
    with open(log_file_path, 'a') as log_file:
        log_file.write(f"{root}\n")

print("Processing completed for all files.")
