# Area Calculator

A Python package for calculating areas of different geometric shapes. The package is designed to be easily extensible for adding new shapes.

## Runtime Polymorphism

The package implements runtime polymorphism, allowing you to work with shapes without knowing their specific type at compile-time. This is achieved through the base `Shape` class and inheritance.

Example of runtime polymorphism:

```python
from area_calculator.shapes.triangle import Triangle
from area_calculator.shapes.circle import Circle

def calculate_total_area(shapes):
    """
    Calculate total area of multiple shapes without knowing their specific types.
    Works with any shape that inherits from Shape class.
    """
    return sum(shape.area() for shape in shapes)

# Create different shapes
shapes = [
    Triangle(3, 4, 5),  # Right triangle
    Circle(5),          # Circle
    Triangle(5, 5, 5),  # Equilateral triangle
]

# Calculate total area without knowing specific types
total_area = calculate_total_area(shapes)
print(f"Total area: {total_area}")

# You can even add new shapes later without modifying this code
shapes.append(Circle(10))
new_total = calculate_total_area(shapes)
```

This demonstrates the key principles:
1. The `calculate_total_area` function works with any shape
2. We don't need to know the specific type of each shape
3. New shapes can be added without modifying existing code
4. The area calculation is determined at runtime, not compile-time

## Installation

```bash
pip install -e .
```

## Usage

### Basic Usage

```python
from area_calculator.shapes.triangle import Triangle
from area_calculator.shapes.circle import Circle

# Create a right triangle (3-4-5)
triangle = Triangle(3, 4, 5)
print(f"Triangle area: {triangle.area()}")  # 6.0
print(f"Is rectangular: {triangle.is_rectangular}")  # True

# Create a circle
circle = Circle(5)
print(f"Circle area: {circle.area()}")  # 78.54...
```

## Adding New Shapes

To add a new shape to the package:

1. Create a new file in `area_calculator/shapes/` directory (e.g., `square.py`)
2. Inherit from the base `Shape` class
3. Implement the required methods

Example of adding a new shape:

```python
from .base import Shape
from ..validators import validate_positive_numbers

class Square(Shape):
    def __init__(self, side):
        validate_positive_numbers(side)
        self.side = side

    def area(self):
        return self.side ** 2
```

Required steps for new shapes:
1. Import the base `Shape` class
2. Use `validate_positive_numbers` for input validation
3. Implement the `area()` method
4. Add appropriate validation for shape-specific properties

## Running Tests

The package uses pytest for testing. To run the tests:

```bash
pytest tests/ -v
```

## Project Structure

```
area_calculator/
├── __init__.py
├── shapes/
│   ├── __init__.py
│   ├── base.py
│   ├── triangle.py
│   └── circle.py
├── validators.py
└── tests/
    └── test_shapes.py
```

## Development

1. Install development dependencies:
```bash
pip install -e ".[dev]"
```

2. Run tests:
```bash
pytest tests/ -v
```

## Contributing

1. Create a new branch for your feature
2. Add your new shape class
3. Add tests for your new shape
4. Submit a pull request

## License

MIT License
