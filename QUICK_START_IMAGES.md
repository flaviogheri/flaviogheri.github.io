# Quick Start: Adding Images to Your Project Pages

## 1. Create Image Directory Structure

```bash
cd /home/fgheri/personal_projects/personal_website

# Create directories
mkdir -p images/imitation_learning
mkdir -p images/malware_detection
mkdir -p images/shared
```

## 2. Where to Find Images (Quick Links)

### For Imitation Learning Page

Copy these search queries into the sites:

| Original Item | Best Source | Search Query |
|--------------|------------|---|
| Robot arm closeup | Unsplash | "robot arm" OR "robotic arm" |
| 3D printer operating | Unsplash | "3D printer" OR "3D printing" |
| Electronics/circuit board | Pixabay | "circuit board" OR "DIY electronics" |
| Servo motors | Pixabay | "servo motor" OR "electronic components" |
| Hands-on assembly | Unsplash | "mechanical assembly" OR "hands building" |
| Data visualization plot | Create your own | Use Python + matplotlib |
| Training curves | Create your own | Copy from your notebook |

**Top Pick for Robot Images:**
- https://huggingface.co/lerobot - Official LeRobot project (check their datasets for SO-100 photos)
- https://github.com/huggingface/lerobot - GitHub repos often have setup photos in README
- Search GitHub: "SO-100 robot imitation learning" - many projects have photos

### For Malware Detection Page

| Element | Best Source | Search Query |
|---------|------------|---|
| Binary/Matrix visual | Unsplash | "binary" OR "code" OR "matrix" |
| Cybersecurity banner | Pexels | "cybersecurity" OR "hacker" |
| Network/Data | Pixabay | "network" OR "data security" |
| Computer/Monitor | Unsplash | "computer" OR "monitor" |
| Confusion Matrix | Create your own | Plot from your results |
| Architecture Diagram | Create your own | Use draw.io |

**Quick Process:**
1. Go to https://unsplash.com
2. Search "robot arm"
3. Find an image you like
4. Download (usually click → Download)
5. Save to `images/imitation_learning/`

## 3. Markdown Syntax for Images

### Basic Image
```markdown
![Brief description](../images/imitation_learning/robot_setup.jpg)
```

### Image with Caption
```markdown
![Robot arm mid-grasp](../images/imitation_learning/robot_grasping.jpg)
*Above: The SO-100 robot arm during object picking demonstration*
```

### Centered Image with Size Control
```markdown
<div style="text-align: center;">
  <img src="../images/imitation_learning/robot_setup.jpg" alt="Robot setup" width="600">
  <p><em>SO-100 robot arm with parallel gripper and camera mounts</em></p>
</div>
```

## 4. Where to Add Images in Each Page

### In Imitation_learning.md

**Suggestion 1: After "Hardware Setup" section**
```markdown
## Hardware Setup

The system was built around an **SO-100 robot** with **parallel gripper end-effector**...

![SO-100 robot complete setup](../images/imitation_learning/so100_complete_setup.jpg)
*Above: Complete SO-100 system with parallel gripper and camera mounts*
```

**Suggestion 2: After "3D Printing and Mechanical Build" section**
```markdown
## 3D Printing and Mechanical Build

A large part of the project was mechanical. I printed and assembled...

<div style="text-align: center;">
  <img src="../images/imitation_learning/3d_printed_parts.jpg" alt="3D printed robot parts" width="600">
  <p><em>3D printed components of the SO-100 arm structure (PETG with 15% cublic infill)</em></p>
</div>
```

**Suggestion 3: After "Electronics" section**
```markdown
## Electronics

On the electronics side, I connected the servo motors...

![Electronics and Teensy board setup](../images/imitation_learning/electronics_wiring.jpg)
*Teensy 4.1 board with servo motor connections and power distribution*
```

**Suggestion 4: After "How I Trained It" section - Training Results**
```markdown
The following visualization shows the training progress:

![Training loss curves](../images/imitation_learning/training_curves.png)
*Training and validation loss over 150 epochs with early stopping*
```

### In malware_detection.md

**Suggestion 1: After "So it works: Binary Visualizer" section**
The interactive scanner is already there! No image needed, users interact with it.

**Suggestion 2: After "Results on the MalImg Dataset" section**
```markdown
The confusion matrices below show detailed performance:

![Confusion Matrix Best Model](../images/malware_detection/confusion_matrix_best.png)
*Above: Confusion matrix of the best performing 3-layer CNN model achieving 98.62% accuracy*
```

**Suggestion 3: After "What I Learned" section**
```markdown
The following chart compares performance across architectures:

![Architecture Comparison](../images/malware_detection/architecture_comparison.png)
*Comparison of 2, 3, and 4-layer CNN architectures on the MalImg dataset*
```

## 5. Creating Your Own Visualizations

### Generate Training Curves (Python)

```python
import matplotlib.pyplot as plt
import numpy as np

# Simulated training data (replace with your actual data)
epochs = np.arange(1, 151)
train_loss = 0.5 * np.exp(-epochs/50) + 0.1 * np.random.random(150)
val_loss = 0.5 * np.exp(-epochs/50) + 0.15 * np.random.random(150)

# Create plot
fig, ax = plt.subplots(figsize=(10, 6), dpi=150)
ax.plot(epochs, train_loss, label='Training Loss', linewidth=2, color='#2a5caf')
ax.plot(epochs, val_loss, label='Validation Loss', linewidth=2, color='#ff6b6b')
ax.set_xlabel('Epoch', fontsize=12)
ax.set_ylabel('Loss', fontsize=12)
ax.set_title('Model Training Progress', fontsize=14, fontweight='bold')
ax.legend(fontsize=11)
ax.grid(True, alpha=0.3)
plt.tight_layout()

# Save
plt.savefig('images/imitation_learning/training_curves.png', dpi=150, bbox_inches='tight')
print("✅ Saved: images/imitation_learning/training_curves.png")
```

### Create Confusion Matrix (Python)

```python
import matplotlib.pyplot as plt
import numpy as np
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay

# Example confusion matrix for 3 object types: red, blue, cube
class_names = ['Red', 'Blue', 'Cube']
# Replace with your actual predictions and ground truth
y_true = [0, 1, 2, 0, 1, 2, 0, 0, 1]
y_pred = [0, 1, 2, 0, 1, 1, 0, 0, 1]

# Create confusion matrix
cm = confusion_matrix(y_true, y_pred)

# Plot
fig, ax = plt.subplots(figsize=(8, 6), dpi=150)
disp = ConfusionMatrixDisplay(confusion_matrix=cm, display_labels=class_names)
disp.plot(ax=ax, cmap='Blues', values_format='d')
plt.title('Object Sorting Accuracy by Type', fontsize=14, fontweight='bold')
plt.tight_layout()

# Save
plt.savefig('images/imitation_learning/confusion_matrix.png', dpi=150, bbox_inches='tight')
print("✅ Saved: images/imitation_learning/confusion_matrix.png")
```

## 6. Using Draw.io for Diagrams

1. Go to https://draw.io
2. Create New → Browser
3. Create diagrams for:
   - Data flow pipeline (data collection → training → deployment)
   - Network architecture (input → encoder → transformer → decoder)
   - Hardware connection diagram (Teensy → servos → sensors)
4. Export as PNG with transparent background
5. Save to `images/[project]/diagram_name.png`

## 7. File Size Optimization

Before adding images, optimize them:

```bash
# Install ImageMagick (optional)
sudo apt-get install imagemagick

# Compress image
convert large_image.jpg -quality 85 -resize 800x600 compressed_image.jpg

# Check file size
ls -lh compressed_image.jpg
```

Or use online tools:
- https://tinypng.com - PNG/JPG compression
- https://imageresizer.com - Resize images online

**Target:** Keep images under 300KB each for web loading

## 8. Complete Example: Adding Image to Page

```markdown
## Hardware Setup

The system was built around an **SO-100 robot** with **parallel gripper end-effector**. 
To make the setup usable for learning, I configured it with:

- **Actuators:** 6 MG90S servo motors (5 for arm DOF, 1 for gripper)
- **Control board:** Teensy 4.1 microcontroller with USB communication
- **Power supply:** 5V/3A switching supply for servo operation
- **Teleoperation method:** Leader arm with matching SO-100 follower
- **Camera setup:** Overlead + wrist-mounted cameras
- **Host machine:** Ubuntu 22.04 laptop with RTX 3060 GPU

![Complete SO-100 setup with cameras and gripper](../images/imitation_learning/so100_hardware.jpg)
*Above: The complete hardware setup showing the arm, gripper, camera mounts, and Teensy control board*

This gave me a complete platform for collecting demonstrations and replaying learned actions 
on the physical robot.
```

## 9. Checklist for Image Integration

- [ ] Create `images/imitation_learning/` directory
- [ ] Create `images/malware_detection/` directory
- [ ] Download 3-5 robot/electronics images
- [ ] Generate your own training plots/curves
- [ ] Create architecture or flow diagrams
- [ ] Add markdown image references to pages
- [ ] Test Jekyll build: `bundle exec jekyll build`
- [ ] View locally: `bundle exec jekyll serve`
- [ ] Check mobile responsiveness
- [ ] Verify all images load correctly

## 10. Tips

✅ **Do:**
- Use consistent image sizes across a page
- Include captions and image descriptions
- Optimize image file sizes
- Test on mobile devices
- Use high-quality sources

❌ **Don't:**
- Use copyrighted images without permission
- Use oversized images (> 1MB each)
- Skip alt text (important for accessibility)
- Mix low-quality with high-quality images

---

## Need Help?

- **Image won't display?** Check path is correct relative to markdown file
- **Page looks broken?** Run `bundle exec jekyll build` to check for errors
- **Image too large?** Use ImageMagick or online tools to compress
- **Uncertain about licensing?** Use CC0 images from Unsplash or Pexels

Good luck! 🎨📸
