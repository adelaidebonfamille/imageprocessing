# Image Processor Application

This repository contains an image processing application built using Python, OpenCV, and IPython. The application allows users to upload an image, perform various processing operations such as resizing, color conversion, blurring, and more, and display the processed images.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [File Structure](#file-structure)

## Features

- Load and display images from your file system
- Perform various image processing operations:
  - Color conversion (original, RGB to BGR, grayscale)
  - Resizing
  - Erosion
  - Blurring
  - Denoising
  - Changing resolution
- Display the processed images using IPython
- Show file size of the image before and after processing

## Installation

Ensure you have Python installed on your machine. You will also need to install the required libraries. You can install the necessary libraries using pip:

```bash
pip install opencv-python numpy pillow ipython
```

For Google Colab, you can use the following:

```python
!pip install opencv-python-headless numpy pillow
```

## Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/adelaidebonfamille/image-processor.git
   cd image-processor
   ```

2. Run the application in an IPython or Jupyter notebook environment:
   ```python
   import cv2
   import numpy as np
   from IPython.display import display, Image
   from google.colab import files
   import os

   # Paste the ImageProcessor class code here

   image_uploaded = False
   image_processor = ImageProcessor()

   while True:
       if not image_uploaded:
           uploaded = files.upload()
           if not uploaded:
               user_input = input("Tidak ada gambar yang diunggah. Apakah ingin mengunggah gambar lagi? (y/n): ").lower()
               if user_input == 'y':
                   continue
               elif user_input == 'n':
                   print("Terima kasih, keluar dari program.")
                   break
               else:
                   print("Input tidak valid, keluar dari program.")
                   break
           image_filename = list(uploaded.keys())[0]
           image_path = "/content/" + image_filename
           try:
               image_processor.load_image(image_path)
               image_uploaded = True
               image_processor.display_image(image_processor.original_image)
               print('Ukuran gambar: ', image_processor.get_file_size(image_processor.original_image))
           except Exception as e:
               print(f"Terjadi kesalahan: {e}")

       menu_option = int(input("Pilih opsi:\n1. Lihat storage size image\n2. Ubah warna image\n3. Resizing image\n4. Erode image\n5. Image blurring\n6. Denoise image\n7. Pilihan resolusi\n8. Ganti Gambar\n9. Keluar\nMasukkan nomor opsi: "))
       if menu_option == 9:
           print("Terima Kasih, Anda keluar dari program")
           break
       image_processor.process_option(menu_option)
   ```

3. Follow the prompts to upload an image and perform various image processing operations.

## File Structure

```
image-processor/
├── image_processor.py
├── README.md
└── LICENSE
```

### image_processor.py

This is the main Python file containing the code for the image processor application. It includes the following key components:

- `ImageProcessor` class: Handles image loading, processing, and displaying.
  - `__init__(self)`: Initializes the class with default attributes.
  - `load_image(self, image_path)`: Loads an image from the specified path.
  - `display_image(self, image, format='.jpg')`: Displays the image in the IPython environment.
  - `get_file_size(self, image)`: Returns the file size of the image in bytes.
  - `change_color(self, color_option)`: Changes the color of the image based on the selected option.
  - `resize_image(self, new_width, new_height)`: Resizes the image to the specified dimensions.
  - `erode_image(self, kernel_size)`: Applies erosion to the image with the specified kernel size.
  - `blur_image(self, blur_size)`: Applies blurring to the image with the specified blur size.
  - `denoise_image(self)`: Applies denoising to the image.
  - `change_resolution(self, new_resolution)`: Changes the resolution of the image.
  - `process_option(self, menu_option)`: Processes the selected menu option and calls the appropriate function.
  - `change_image(self)`: Allows the user to change the image.

## Contributing

Contributions are welcome! If you have any suggestions or improvements, please open an issue or submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Enjoy using the image processor application! If you encounter any issues, feel free to open an issue in this repository.
