# 🖼️ Bulk Image Background Remover using Python

This script processes images in a specified folder and removes their background using the `rembg` library. The output images are saved in PNG format, ensuring transparency is preserved.

## 🚀 Features
- ✅ Automatically removes the background from images
- ✅ Supports multiple formats: `.png`, `.jpg`, `.jpeg`, `.bmp`, `.gif`
- ✅ Saves output images in PNG format for transparency
- ✅ Easy to use with a simple folder-based input/output system

## 📦 Installation

Ensure you have Python installed, then install the required dependencies:
```sh
pip install rembg pillow
```

## 📜 Usage

Place all the images you want to process inside the `Logo New 2025` folder, then run the script:

```python
import os
import io
from rembg import remove
from PIL import Image

# Define paths
input_folder = './Logo New 2025'
output_folder = './removed background from images'

# Create the output folder if it doesn't exist
if not os.path.exists(output_folder):
    os.makedirs(output_folder)

# Loop through all files in the input folder
for filename in os.listdir(input_folder):
    file_path = os.path.join(input_folder, filename)

    # Check if it's an image file
    if filename.lower().endswith(('.png', '.jpg', '.jpeg', '.bmp', '.gif')):
        try:
            # Open the image
            with open(file_path, 'rb') as input_file:
                input_image = input_file.read()

            # Remove background
            output_image = remove(input_image)

            # Convert to PNG format (supports transparency)
            output_image = Image.open(io.BytesIO(output_image))
            output_image = output_image.convert("RGBA")

            # Save the output image
            output_file_path = os.path.join(output_folder, filename)
            if not output_file_path.lower().endswith('.png'):
                output_file_path = os.path.splitext(output_file_path)[0] + '.png'
            
            output_image.save(output_file_path, format='PNG')

            print(f"Processed and saved: {filename}")
        except Exception as e:
            print(f"Error processing {filename}: {e}")

print("Background removal process complete.")
```

## 📂 Output
The processed images with removed backgrounds will be saved in the `removed background from images` folder.

## 🔗 Contribute
Feel free to submit issues or pull requests to enhance this script.

⭐ **Star this repo** if you find it useful!
