# rgb_color_picker

A simple Python project to generate a range of RGB color codes by blending a base color with gray, useful for creating color gradients or palettes for data visualization.

## Features

- Blends a specified base RGB color with gray across 10 evenly spaced thresholds (10% increments).
- Outputs a DataFrame listing the resulting RGB values for each bracket.
- Easy to modify for different base or blend colors.

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/martinedb/rgb_color_picker.git
   cd rgb_color_picker
   ```

2. **Install dependencies**  
   This project uses [pandas](https://pandas.pydata.org/). Install it via pip:
   ```bash
   pip install pandas
   ```

## Usage

Open the Jupyter notebook `rgb_color_picker.ipynb` to run or modify the color blending logic.

Or, run the relevant code in your own Python script:
```python
import pandas as pd

# Define base and gray colors
base_color = {'R': 190, 'G': 80, 'B': 20}
gray_color = {'R': 191, 'G': 191, 'B': 191}

# Create thresholds for 0-10%, 10-20%, ..., 90-100%
thresholds = [i/10 for i in range(1, 11)]  # 0.1 to 1.0

# Compute blended colors for each threshold
data = []
for t in thresholds:
    blended_r = round(base_color['R'] * (1 - t) + gray_color['R'] * t)
    blended_g = round(base_color['G'] * (1 - t) + gray_color['G'] * t)
    blended_b = round(base_color['B'] * (1 - t) + gray_color['B'] * t)
    data.append({'UpperBound (%)': f"{int(t*100)}%", 'R': blended_r, 'G': blended_g, 'B': blended_b})

df = pd.DataFrame(data)
print(df)
```

## Example Output

| UpperBound (%) |   R   |   G   |   B   |
|:--------------:|:-----:|:-----:|:-----:|
|      10%       | 190   | 91    | 38    |
|      20%       | 190   | 103   | 56    |
|      ...       | ...   | ...   | ...   |
|     100%       | 191   | 191   | 191   |

## License

This project is licensed under the terms of the [MIT License](LICENSE).
