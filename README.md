# Edge Detection Using OpenCV

---

## Aim

To perform edge detection using Sobel, Laplacian, and Canny edge detectors.

The program also implements Prewitt and Roberts edge detectors as included in the template repository.

---

## Software Required

- Anaconda – Python 3.7
- Jupyter Notebook / VS Code
- OpenCV (`cv2`)
- NumPy
- Matplotlib

---

## Algorithm

### Step 1:

Import all the necessary libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:

Load an input image using `cv2.imread()`.

### Step 3:

Convert the image to grayscale using `cv2.cvtColor()`.

### Step 4: Sobel Edge Detector

- Apply the Sobel operator in the horizontal direction.
- Apply the Sobel operator in the vertical direction.
- Combine the gradients to display the edges.

### Step 5: Prewitt Edge Detector

- Create horizontal and vertical Prewitt kernels.
- Apply the kernels using `cv2.filter2D()`.
- Combine the results to obtain the edge map.

### Step 6: Roberts Edge Detector

- Create diagonal Roberts kernels.
- Apply the kernels using `cv2.filter2D()`.
- Combine the gradients to detect diagonal edges.

### Step 7: Laplacian Edge Detector

- Apply the Laplacian operator using `cv2.Laplacian()`.
- Display the detected edges.

### Step 8: Canny Edge Detector

- Apply Canny edge detection using `cv2.Canny()`.
- Display the resulting edge image.

### Step 9:

Display the original grayscale image and the detected edge images for comparison.

---

## Developed By

- **Name:** Shaajini N
- **Register No:** 212225040395

---

## Program

### Program 1: Sobel Edge Detector

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

image_path = r"C:\Users\acer\images\Boy.jpg"
img = cv2.imread(image_path)

if img is None:
    print("Error: Image not found. Check the image path.")
else:
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    sobel_x = cv2.Sobel(
        gray, cv2.CV_64F, 1, 0, ksize=3
    )
    sobel_y = cv2.Sobel(
        gray, cv2.CV_64F, 0, 1, ksize=3
    )

    abs_x = cv2.convertScaleAbs(sobel_x)
    abs_y = cv2.convertScaleAbs(sobel_y)

    sobel_combined = cv2.addWeighted(
        abs_x, 0.5, abs_y, 0.5, 0
    )

    plt.figure(figsize=(12, 4))

    plt.subplot(1, 3, 1)
    plt.imshow(gray, cmap="gray")
    plt.title("Original Grayscale")
    plt.axis("off")

    plt.subplot(1, 3, 2)
    plt.imshow(abs_x, cmap="gray")
    plt.title("Sobel X")
    plt.axis("off")

    plt.subplot(1, 3, 3)
    plt.imshow(sobel_combined, cmap="gray")
    plt.title("Sobel Edge Detection")
    plt.axis("off")

    plt.tight_layout()
    plt.show()
```

### Program 2: Prewitt Edge Detector

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

image_path = r"C:\Users\acer\images\Boy.jpg"
img = cv2.imread(image_path)

if img is None:
    print("Error: Image not found. Check the image path.")
else:
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    kernel_x = np.array([
        [-1, 0, 1],
        [-1, 0, 1],
        [-1, 0, 1]
    ], dtype=np.float32)

    kernel_y = np.array([
        [-1, -1, -1],
        [0, 0, 0],
        [1, 1, 1]
    ], dtype=np.float32)

    prewitt_x = cv2.filter2D(
        gray, cv2.CV_32F, kernel_x
    )
    prewitt_y = cv2.filter2D(
        gray, cv2.CV_32F, kernel_y
    )

    magnitude = cv2.magnitude(prewitt_x, prewitt_y)
    prewitt = cv2.convertScaleAbs(magnitude)

    plt.figure(figsize=(10, 4))

    plt.subplot(1, 2, 1)
    plt.imshow(gray, cmap="gray")
    plt.title("Original Grayscale")
    plt.axis("off")

    plt.subplot(1, 2, 2)
    plt.imshow(prewitt, cmap="gray")
    plt.title("Prewitt Edge Detection")
    plt.axis("off")

    plt.tight_layout()
    plt.show()
```

### Program 3: Roberts Edge Detector

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

image_path = r"C:\Users\acer\images\Boy.jpg"
img = cv2.imread(image_path)

if img is None:
    print("Error: Image not found. Check the image path.")
else:
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    kernel_x = np.array([
        [1, 0],
        [0, -1]
    ], dtype=np.float32)

    kernel_y = np.array([
        [0, 1],
        [-1, 0]
    ], dtype=np.float32)

    roberts_x = cv2.filter2D(
        gray, cv2.CV_32F, kernel_x
    )
    roberts_y = cv2.filter2D(
        gray, cv2.CV_32F, kernel_y
    )

    magnitude = cv2.magnitude(roberts_x, roberts_y)
    roberts = cv2.convertScaleAbs(magnitude)

    plt.figure(figsize=(10, 4))

    plt.subplot(1, 2, 1)
    plt.imshow(gray, cmap="gray")
    plt.title("Original Grayscale")
    plt.axis("off")

    plt.subplot(1, 2, 2)
    plt.imshow(roberts, cmap="gray")
    plt.title("Roberts Edge Detection")
    plt.axis("off")

    plt.tight_layout()
    plt.show()
```

### Program 4: Laplacian Edge Detector

```python
import cv2
import matplotlib.pyplot as plt

image_path = r"C:\Users\acer\images\Boy.jpg"
img = cv2.imread(image_path)

if img is None:
    print("Error: Image not found. Check the image path.")
else:
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    laplacian = cv2.Laplacian(
        gray, cv2.CV_64F, ksize=3
    )
    laplacian_abs = cv2.convertScaleAbs(laplacian)

    plt.figure(figsize=(10, 4))

    plt.subplot(1, 2, 1)
    plt.imshow(gray, cmap="gray")
    plt.title("Original Grayscale")
    plt.axis("off")

    plt.subplot(1, 2, 2)
    plt.imshow(laplacian_abs, cmap="gray")
    plt.title("Laplacian Edge Detection")
    plt.axis("off")

    plt.tight_layout()
    plt.show()
```

### Program 5: Canny Edge Detector

```python
import cv2
import matplotlib.pyplot as plt

image_path = r"C:\Users\acer\images\Boy.jpg"
img = cv2.imread(image_path)

if img is None:
    print("Error: Image not found. Check the image path.")
else:
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    canny = cv2.Canny(
        gray, threshold1=100, threshold2=200
    )

    plt.figure(figsize=(10, 4))

    plt.subplot(1, 2, 1)
    plt.imshow(gray, cmap="gray")
    plt.title("Original Grayscale")
    plt.axis("off")

    plt.subplot(1, 2, 2)
    plt.imshow(canny, cmap="gray")
    plt.title("Canny Edge Detection")
    plt.axis("off")

    plt.tight_layout()
    plt.show()
```

---

## Output

### Sobel Edge Detector

- Detects edges in horizontal and vertical directions.
- Produces a gradient-based edge map.

**Output Screenshot:** Add the Sobel output screenshot here.

### Prewitt Edge Detector

- Detects edges using horizontal and vertical Prewitt kernels.

**Output Screenshot:** Add the Prewitt output screenshot here.

### Roberts Edge Detector

- Detects edges using diagonal gradient kernels.
- Highlights diagonal intensity changes.

**Output Screenshot:** Add the Roberts output screenshot here.

### Laplacian Edge Detector

- Detects edges using second-order derivatives.
- Highlights rapid intensity changes.

**Output Screenshot:** Add the Laplacian output screenshot here.

### Canny Edge Detector

- Detects edges using a multi-stage algorithm.
- Produces clear, thin edge boundaries.

**Output Screenshot:** Add the Canny output screenshot here.

---

## Result

Thus, edge detection is performed successfully using Sobel, Prewitt, Roberts, Laplacian, and Canny edge detection techniques. Each method detects edges differently based on intensity variations and gradient information, supporting feature extraction and image analysis.
