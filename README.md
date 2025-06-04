# AWS DeepRacer Track Visualization

This repository contains visualizations and analysis of AWS DeepRacer track data, specifically focusing on the Re:Invent base track. The project demonstrates how to download, process, and visualize track waypoint data using Python.

## 🏁 Project Overview

This project showcases various visualization techniques for AWS DeepRacer track data, creating multiple perspectives of the same track layout without overwhelming surface details. All visualizations focus on clean line-based representations suitable for analysis and development.

## 📁 Repository Contents

### Data Files
- `reinvent_base.npy` - Original track waypoint data from AWS DeepRacer community repository

### Generated Visualizations
- `reinvent_base_track.png` - Basic track layout with center line and boundaries
- `reinvent_base_track_4subplots.png` - Four different perspectives in subplot format
- `reinvent_base_track_with_indices.png` - Detailed track map with numbered waypoints (0-118)

### Source Code
- `aws_deepracer_track_visualization.ipynb` - Complete Jupyter notebook with all code and documentation

## 🤖 Interpreter Usage History

This project was developed using Open Interpreter, an AI-powered code execution environment. Below is the detailed history of commands and interactions:

### Session Overview
The development process involved multiple iterations to create clean, professional visualizations while avoiding display issues that could crash the interpreter.

### Key Interpreter Commands Used

#### 1. Initial Data Download
```bash
wget https://github.com/aws-deepracer-community/deepracer-race-data/raw/refs/heads/main/raw_data/tracks/npy/reinvent_base.npy
```
- **Purpose**: Download track data from AWS DeepRacer community repository
- **Result**: Successfully obtained 119-waypoint track data (5,840 bytes)

#### 2. Data Analysis
```python
import numpy as np
track_data = np.load('reinvent_base.npy')
print(f"Track data shape: {track_data.shape}")
```
- **Purpose**: Load and examine track structure
- **Discovery**: 119 waypoints × 6 coordinates (center, left boundary, right boundary)

#### 3. Basic Visualization (Attempt 1)
```python
plt.figure(figsize=(12, 8))
plt.plot(x_center, y_center, 'b-', linewidth=3, label='Center Line')
plt.plot(x_left, y_left, 'r-', linewidth=2, label='Left Boundary')  
plt.plot(x_right, y_right, 'g-', linewidth=2, label='Right Boundary')
plt.fill_between(x_left, y_left, x_right, y_right, alpha=0.3, color='gray', label='Track Surface')
plt.show()  # ❌ CAUSED INTERPRETER TO QUIT
```
- **Issue**: Using `plt.show()` caused GUI display problems and interpreter crash
- **Learning**: GUI display can be problematic in certain environments

#### 4. Solution Development
```python
plt.savefig('reinvent_base_track.png', dpi=300, bbox_inches='tight', 
            facecolor='white', edgecolor='none')
plt.close()  # ✅ PREVENTS DISPLAY ISSUES
```
- **Solution**: Use `plt.savefig()` + `plt.close()` instead of `plt.show()`
- **Benefit**: Creates high-quality files without display crashes

#### 5. Four Subplot Creation
```python
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(16, 12))
# Multiple subplot configurations without track surface fill
```
- **Request**: Create 4 subplots without track surface information
- **Implementation**: Different perspectives (center only, boundaries only, combined, with waypoints)

#### 6. Detailed Index Mapping
```python
# Add index numbers for each point on the center line
for i in range(len(x_center)):
    plt.annotate(str(i), xy=(x_center[i], y_center[i]), ...)
```
- **Purpose**: Show waypoint indices for detailed track analysis
- **Result**: Large format map (20×14) with all 119 points labeled

#### 7. Notebook Creation
```python
notebook_content = {...}  # Comprehensive Jupyter notebook structure
with open('aws_deepracer_track_visualization.ipynb', 'w') as f:
    json.dump(notebook_content, f, indent=2)
```
- **Purpose**: Create self-contained documentation with all code
- **Features**: Markdown explanations, runnable code cells, image references

### 🔧 Technical Challenges & Solutions

| Challenge | Solution | Learning |
|-----------|----------|----------|
| Interpreter crashes on `plt.show()` | Use `plt.savefig()` + `plt.close()` | GUI display can be problematic |
| Display module errors | Work around with direct file operations | Dependencies may have issues |
| Track surface visual clutter | Remove fill, focus on line art | Clean visualizations are more professional |
| Waypoint identification | Add numbered annotations | Index mapping aids development |

### 🎯 Best Practices Developed

1. **Always use `plt.close()`** after saving to prevent memory/display issues
2. **High DPI settings** (300) for professional quality output
3. **Avoid track surface fills** for cleaner technical diagrams
4. **Consistent color coding**: Blue=center, Red=left, Green=right
5. **Professional styling** with legends, grids, and proper labels

### 📊 Code Execution Statistics

- **Total commands executed**: ~15 code blocks
- **Files generated**: 5 (1 data + 3 PNG + 1 notebook)
- **Total file size**: ~1.7 MB
- **Successful visualizations**: 3 different styles
- **Zero display crashes** after implementing `plt.close()` pattern

## 🚀 Quick Start

1. **Clone this repository**
   ```bash
   git clone https://github.com/itemhsu/2018track.git
   cd 2018track
   ```

2. **Install dependencies**
   ```bash
   pip install numpy matplotlib jupyter
   ```

3. **Run the notebook**
   ```bash
   jupyter notebook aws_deepracer_track_visualization.ipynb
   ```

4. **Or run individual sections** to generate specific visualizations

## 📈 Track Data Structure

The `.npy` files contain waypoint data with 6 columns per point:
- **Columns 0,1**: Center line coordinates (x, y) 
- **Columns 2,3**: Left boundary coordinates (x, y)
- **Columns 4,5**: Right boundary coordinates (x, y)

**Re:Invent Base Track Specifications:**
- Total waypoints: 119 (indexed 0-118)
- Track format: Closed loop
- Coordinate system: Meters
- Data source: AWS DeepRacer Community Repository

## 🎨 Visualization Features

### Basic Track Layout
- Clean line-based representation
- Color-coded boundaries and center line
- Professional grid and labeling

### Four Subplot Analysis
- Center line isolation
- Boundary-only view  
- Complete combined layout
- Waypoint sampling visualization

### Detailed Index Mapping
- All 119 waypoints numbered
- Start/finish point highlighted
- Large format for detailed analysis
- Professional annotations with backgrounds

## 🤝 Contributing

Feel free to:
- Add visualizations for other tracks
- Improve the styling and layouts
- Create interactive versions
- Add analysis features

## 📜 License

This project uses publicly available AWS DeepRacer community data. See individual file headers for specific licensing information.

## 🙏 Acknowledgments

- AWS DeepRacer Community for providing track data
- Open Interpreter for enabling rapid development
- Matplotlib for excellent visualization capabilities

---

*Generated using Open Interpreter - AI-powered code execution and development*
