# Death Star Ray Tracer

A Python ray tracer built to explore the mathematics behind 3D computer graphics by rendering the **Death Star from Star Wars**.

This project accompanies my Mathematics Internal Assessment, *An Exploration of the Mathematics in Ray Tracing the Death Star from Star Wars*. Rather than using a 3D modeling or rendering engine, it constructs a simplified Death Star from geometric primitives and calculates ray–object intersections mathematically.

## Features

- **Ray casting:** Sends rays from a virtual camera through a viewport to determine visible surfaces.
- **Geometric intersections:** Solves intersections with spheres, circular disks, and finite cones.
- **Constructive geometry:** Uses a *negative cone* to remove parts of the sphere and reveal the recessed superlaser dish.
- **Vector-based lighting:** Uses surface normals and a light-direction vector for grayscale shading.
- **Camera rotation:** Produces a sequence of views around the Death Star and assembles them into an MP4 animation.
- **NumPy-based mathematics:** Uses vectors, dot products, cross products, and rotation matrices.

## How it works

For each sampled point on the viewport, the program constructs a ray:

$$
\mathbf{P}(t)=\mathbf{O}+t\mathbf{D}
$$

where $\mathbf{O}$ is the camera position, $\mathbf{D}$ is the normalized ray direction, and $t$ is the distance parameter.

The ray is tested against the scene's three positive shapes:

| Shape | Purpose | Intersection approach |
| --- | --- | --- |
| Sphere | Main body of the Death Star | Substitute the ray equation into the sphere equation and solve a quadratic |
| Cone | Superlaser dish geometry | Solve a quadratic and restrict intersections to the cone's direction and finite height |
| Circle | Circular feature inside the dish | Intersect the ray with a plane, then check the radial distance |

Candidate intersections inside the **negative cone** are ignored to create the recessed region. The program applies grayscale intensity using the dot product of a light-direction vector and a surface normal.

The model uses geometric measurements discussed in the accompanying Math IA:

| Parameter | Value |
| --- | ---: |
| Sphere radius | 1281 units |
| Cone base radius | 340 units |
| Circle radius | 28.6 units |
| Cone surface angle | 76.7° |
| Cone-axis orientation | 23° |
| Camera field of view | 60° |

These values represent the project's modeling coordinates, not a claim about the Death Star's physical dimensions.

## Requirements

- Python 3
- [NumPy](https://numpy.org/)
- [Matplotlib](https://matplotlib.org/)
- [tqdm](https://tqdm.github.io/) (imported by the current script)
- [FFmpeg](https://ffmpeg.org/) available to Matplotlib for MP4 export

## Installation

Clone the repository and install the Python dependencies:

```bash
git clone https://github.com/tin-martin/Ray-Tracer.git
cd Ray-Tracer
python -m pip install numpy matplotlib tqdm
```

Install FFmpeg separately and ensure that `ffmpeg` is available on your system's `PATH`.

## Usage

Run the renderer from the repository directory:

```bash
python main.py
```

The script generates **37 frames**, rotating the view by **10°** between frames. It saves the animation as `movie1.mp4` in the working directory and then opens a Matplotlib window to display the result. Rendering may take some time because intersections are computed in Python for each sampled viewport position.

You can experiment with the configuration in `main.py`:

- `FOV`: camera field of view
- `scene1.div`: sampling interval (smaller values produce a more detailed but slower render)
- `rSphere`, `rCone`, `rCircle`: geometric dimensions
- `theta` and `beta`: cone geometry and orientation
- `lv`: lighting direction
- `scene1.changeAngleX/Y/Z(...)`: rotation matrices used to adjust ray directions

## Project structure

```text
Ray-Tracer/
├── main.py       # Scene setup, intersection functions, ray tracer, and animation
└── README.md     # Project documentation
```

The implementation is organized around the `Scene`, `Camera`, `ViewPort`, `Sphere`, `Cone`, and `Circle` classes.

## Mathematical background

My Math IA develops the geometry behind this implementation: parametric rays; quadratic equations for sphere and cone intersections; plane and circle intersections; subtraction of negative shapes; positioning the Death Star components; camera and viewport geometry; and lighting.

The aim is to make the mathematics behind rendering understandable by applying it to a recognizable object. This is an educational renderer rather than a production-ready physically based ray tracer: it uses a simplified geometric model and directional grayscale shading, without realistic reflections or global illumination.

## Author

**Martin Tin**

Developed as an exploration of mathematics, computer graphics, and *Star Wars*.

*Star Wars* and the Death Star are associated with Lucasfilm. This is an independent educational project and is not affiliated with or endorsed by Lucasfilm or Disney.
