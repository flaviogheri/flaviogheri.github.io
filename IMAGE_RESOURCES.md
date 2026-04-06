# Image Resource Guide for Your Project Pages

## For the Imitation Learning (SO-100 Robot) Project

### Best Blog/Tutorial Images to Download

If you want the page to feel concrete and technical, these are the most useful images to grab from LeRobot/SO-100 blogs and tutorials:

1. **Assembled SO-100 robot photo**
   - Use this as the hero image for the page.
   - Look for a full-arm shot with the gripper visible.

2. **Teleoperation setup screenshot**
   - Leader arm and follower arm shown together.
   - Good for explaining how demonstrations were collected.

3. **Wiring / electronics bench photo**
   - Teensy board, servo wiring, power supply, and cables.
   - Great for the Electronics section.

4. **3D-printed parts / assembly photo**
   - Print bed, printed links, joints, or partially assembled arm.
   - Good for the Mechanical Build section.

5. **Dataset / recording screenshot**
   - Camera view with the robot and object setup.
   - Useful for explaining imitation learning data collection.

6. **Training curve / evaluation plot**
   - Use your own plot if possible.
   - If the blog includes a training summary figure, that also works with attribution.

7. **Failure case or success case image**
   - One image showing the robot grasping correctly and one showing a failure.
   - Makes the page feel like a real experiment, not just a polished demo.

### Good Sources for Those Images

- LeRobot GitHub README and documentation
- Hugging Face LeRobot hardware/setup guides
- SO-100 community tutorials and blog posts
- Any project log where the author shows the physical build, not just final results

### What to Prefer

- Prefer images that show the actual robot hardware rather than generic robot stock photos.
- Prefer photos with visible wiring, camera placement, and the workbench setup.
- Prefer screenshots of real demonstrations over abstract diagrams when possible.
- Always add a caption so the reader knows what part of the workflow they are seeing.

### Free Stock Photo Sites (Attribution usually not required for personal projects)

1. **Unsplash** (https://unsplash.com)
   - Search: "robot arm", "3D printing", "hardware electronics"
   - High-quality images, CC0 license
   - Perfect for: arm closeups, electronics workbench, 3D printer in action

2. **Pexels** (https://www.pexels.com)
   - Search: "robotics", "circuit board", "mechanical parts"
   - Free commercial use, CC0
   - Good for: hardware setup, soldering, PCB boards

3. **Pixabay** (https://pixabay.com)
   - Search: "robot", "servo motor", "gripper"
   - Huge collection of tech-related imagery
   - Good for: covering different robot parts

### Specific Robot/Robotics Image Sites

4. **Open Robotics** (https://www.openrobotics.org)
   - Official ROS/robotics community resources
   - May have SO-100 related content or inspiration
   - BSD license

5. **GitHub Robot Projects** (https://github.com/search?q=SO-100&type=repositories)
   - Search for SO-100 robot projects on GitHub
   - Many have photos in their README files
   - Check the license - often MIT or Apache 2.0

6. **Hugging Face LeRobot** (https://huggingface.co/lerobot)
   - Official LeRobot community page
   - Official SO-100 robot images and documentation
   - CC license (check specific dataset licenses)

### For Diagrams and Technical Illustrations

7. **Draw.io** / **Excalidraw** (https://excalidraw.com)
   - Create your own diagrams of robot architecture, data flow
   - Free, no attribution needed if you made it yourself

8. **TensorFlow/PyTorch Documentation**
   - Official architecture diagrams for neural networks
   - Often available under open licenses

9. **Wikimedia Commons** (https://commons.wikimedia.org)
   - Search: "servo motor", "robot arm", "gripper"
   - Various licenses - check each image
   - Usually good quality technical images

### Realistic SO-100 Specific Suggestions

For authentic SO-100 images, look for:
- **LeRobot GitHub Issues/PRs** - community members often post their builds
- **Reddit r/robotics** - SO-100 builds frequently shared
- **Twitter LeRobotHF** (https://twitter.com/LeRobotHF) - official project updates
- **YouTube tutorials** - screenshot relevant parts (check licensing)

---

## For the Malware Detection Project

### Visualization and Technical Images

1. **Unsplash** (https://unsplash.com)
   - Search: "binary code", "cybersecurity", "network", "computer"
   - Good for banner/hero images

2. **Pexels** (https://www.pexels.com)
   - Search: "hacker", "security", "data"
   - Free for any use

3. **Pixabay** (https://pixabay.com)
   - Search: "virus", "malware", "security", "computer"
   - Extensive collection

### Tech-Specific Stock Sites

4. **Unsplash Collections** - "Cyber Security" and "Data Science"
   - Curated collections of relevant images

5. **Icons8** (https://icons8.com) - Icons for malware, virus, scanning
   - Free tier available with attribution
   - Perfect for alerting, virus, scan icons

6. **Font Awesome** (https://fontawesome.com)
   - Free SVG icons for: shield, virus, scan, check, xmark
   - MIT license

### Academic/Research Sources

7. **Research Papers with Figures** (https://arxiv.org)
   - Search: "malware detection CNN"
   - Check paper licenses - most allow reuse in academic context
   - Include proper citations

8. **ImageNet Visualizations**
   - Malware-as-image visualizations are available in academic papers
   - Many show real binary->image transforms
   - Check paper permissions

### Creating Your Own

9. **Your Code + Matplotlib/Seaborn**
   - Generate your own malware binary visualization
   - Create confusion matrices of your results
   - Train/loss curves from your experiments
   - This is ALWAYS the best option for project pages!

10. **Screenshot Your Simulator**
    - Take screenshots of your interactive malware scanner
    - Show different text inputs and their visualizations
    - Makes the page more engaging

---

## Licensing Recommendations

### Safe Practices for Personal Project Pages

✅ **Always Safe:**
- CC0 (Unsplash, Pexels) - no attribution needed
- Your own creations (screenshots, diagrams, plots)
- Images explicitly licensed for personal use
- Images in public domain

⚠️ **Check License:**
- Most free stock sites require attribution (mention in image caption)
- Academic papers - include citation
- GitHub projects - include original project link

❌ **Avoid:**
- Copyrighted movie/game screenshots
- Professional photos without license
- Research images without permission

---

## Implementation Tips

### Adding Images to Your Markdown

```markdown
![Brief description of image](../images/robot_arm.jpg)

![Robot arm during object sorting task](/images/imitation_learning_robot.jpg)
```

### Creating Project Folders

```
personal_website/
├── projects/
│   ├── imitation_learning.md
│   ├── malware_detection.md
│   └── assets/
│       ├── imitation_learning/
│       │   ├── robot_setup.jpg
│       │   ├── 3d_printer.jpg
│       │   └── training_results.png
│       └── malware_detection/
│           ├── binary_visualization.png
│           ├── confusion_matrix.png
│           └── architecture_diagram.png
```

### Recommended Image Specifications

- **Width:** 600-800px for text documents
- **Format:** JPG for photos, PNG for diagrams
- **Resolution:** 72-150 DPI for web
- **Size:** Keep under 500KB per image
- **Alt text:** Always include descriptions for accessibility

---

## Quick Reference Links

- Unsplash: https://unsplash.com
- Pexels: https://www.pexels.com
- Pixabay: https://pixabay.com
- LeRobot: https://huggingface.co/lerobot
- Excalidraw: https://excalidraw.com
- Icons8: https://icons8.com
- Font Awesome: https://fontawesome.com

---

## Pro Tips

1. **Use images consistently:** Keep a consistent style/filter across pages
2. **Screenshot your work:** The best images are your own projects running
3. **Create diagrams:** Data flow, architecture, loss curves tell your story
4. **Caption everything:** Captions help SEO and accessibility
5. **Optimize images:** Use tools like TinyPNG to compress without quality loss
6. **Consider light/dark mode:** Make sure images are visible in both themes

Good luck with your projects! 🚀
