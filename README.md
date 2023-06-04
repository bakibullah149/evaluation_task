# ****evaluation_task****


# ****Blender & Python****

Q1.1: Blender provides an API that can be interacted with using Python. How can you use Python scripting to automate the creation of a 3D model in Blender? Please provide a basic code example.

`Answer`: Blender, the popular open-source 3D computer graphics software, provides an API (Application Programming Interface) that allows users to interact with Blender's functionalities programmatically using the Python programming language.

The Blender Python API enables us to automate tasks, create custom tools and add-ons, manipulate objects, materials, textures, and perform various operations within Blender. It provides access to a wide range of features and functionality, making it a powerful tool for scripting and extending Blender's capabilities.

The Blender Python API allows us to create, modify, and delete objects; manipulate object properties; access and edit materials and textures; perform animations; render scenes; and much more. The API provides a comprehensive set of classes, functions, and modules that allow us to control almost every aspect of Blender.

Leveraging the Blender Python API can extend Blender's functionality, automate repetitive tasks, create custom workflows, and integrate Blender with other tools and software, enabling greater flexibility and efficiency in 3D graphics projects.

Here's a basic code example that demonstrates how we can use Python scripting to automate the creation of a simple 3D model in Blender:

We can start by importing `bpy` and clearing the default scene to remove any existing objects.
```javascript
import bpy

# Clear the default scene
bpy.ops.object.select_all(action='DESELECT')
bpy.ops.object.select_by_type(type='MESH')
bpy.ops.object.delete()
```
Then, we can create a new cube mesh using the `primitive_cube_add` function. We can assign the active object to the `cube` variable for further manipulation.
```javascript
# Create a new mesh object
bpy.ops.mesh.primitive_cube_add(size=2)

# Get a reference to the newly created cube object
cube = bpy.context.active_object
```
Next, we can move the cube to a different location by modifying its `location` property.
```javascript
# Move the cube to a different location
cube.location = (0, 0, 2)
```
After that, we can create a new material and set its color to red. We can append the material to the cube's materials list using `cube.data.materials.append(material)`.
```javascript
# Create a new material
material = bpy.data.materials.new(name="Red")
material.diffuse_color = (1, 1, 1, 1)  # Set the material color to red

# Assign the material to the cube
cube.data.materials.append(material)
```
To set up rendering, we can set the render engine to Cycles and configure the render settings such as output format and file path. Finally, we use `bpy.ops.render.render` to render the scene and save the output to the specified file path.
```javascript
# Set the render engine to Cycles
bpy.context.scene.render.engine = 'CYCLES'

# Set up the render settings
bpy.context.scene.render.image_settings.file_format = 'PNG'
bpy.context.scene.render.filepath = "/path/to/output/file.png"

# Render the scene
bpy.ops.render.render(write_still=True)
```
This is just a simple example, but with the Blender Python API, we can perform more complex operations, create and modify various types of objects, apply transformations, manipulate materials and textures, and much more to automate the creation of intricate 3D models in Blender.

Q1.2: In Blender's Python API, what is the purpose of the `bpy` module? How can you use it to manipulate object transformations in a 3D scene?

`Answer`: In the Blender Python API, the `bpy` module is a fundamental module that serves as the entry point for accessing Blender's data and functionality through Python scripting. It provides a wide range of classes, functions, and properties to interact with various aspects of Blender.

Here are some key purposes of the `bpy` module in Blender's Python API:

- Scene and Data Access: The `bpy.data` sub-module within `bpy` allows us to access and manipulate various types of data in Blender, such as scenes, objects, materials, textures, animations, and more. It provides methods to create, modify, and delete data elements within the Blender environment.

- Operator Execution: The `bpy.ops` sub-module provides access to operators, which are predefined functions that execute specific actions or operations in Blender. These operators replicate functionalities that can be accessed through the user interface, allowing us to automate tasks by invoking them from Python scripts.

- Context and Execution Environment: The `bpy.context` module allows us to access information about the current execution context, such as the active scene, selected objects, render settings, and more. It provides a way to interact with Blender's current state and retrieve or modify properties related to the current context.

- User Interface Interaction: While Blender's Python API primarily focuses on scripting and automation, the `bpy` module also provides access to some aspects of the user interface. We can create custom panels, menus, and operators, define keymaps, and interact with user interface elements within the scripting environment.

- File I/O and System Integration: The `bpy.data` module within `bpy` also includes methods for reading and writing data in various formats, allowing us to import and export data from external sources. Additionally, Blender's Python API provides ways to interact with the operating system, perform file operations, and execute external commands.

Overall, the `bpy` module in Blender's Python API acts as a bridge between the Python scripting environment and Blender, offering a comprehensive set of functionalities to create, manipulate, and interact with 3D data, scenes, and settings in Blender.

To manipulate object transformations in a 3D scene using the Blender Python API, we can access and modify various properties of the objects, such as their location, rotation, and scale. Here's an example that demonstrates how to manipulate object transformations:

- Importing the necessary modules:
```javascript
import bpy
import math
import mathutils
```
- Creating a new cube object:
```javascript
bpy.ops.mesh.primitive_cube_add(size=2)
cube = bpy.context.active_object
```
This code uses Blender's operators to add a cube primitive with a size of 2. The `bpy.context.active_object` variable stores the reference to the newly created cube object.

- Translating the cube:
```javascript
cube.location = (2, 0, 0)
```
Here, the `location` attribute of the cube object is set to `(2, 0, 0)`, which moves the cube 2 units along the X-axis.

- Rotating the cube:
```javascript
rotation_angle = math.radians(45)
cube.rotation_euler = (rotation_angle, 0, 0)
```
The `rotation_euler` attribute of the cube object is set to `(rotation_angle, 0, 0)`, where `rotation_angle` is converted from degrees to radians using the `math.radians()` function. This rotates the cube by 45 degrees around the X-axis.

- Scaling the cube:
```javascript
cube.scale = (1.5, 1, 1)
```
The `scale` attribute of the cube object is set to `(1.5, 1, 1)`, which scales the cube by a factor of 1.5 along the X-axis.

- Appling a transformation matrix to the cube:
```javascript
translation_matrix = mathutils.Matrix.Translation((0, 0, 2))
rotation_matrix = mathutils.Matrix.Rotation(rotation_angle, 4, 'X')
scale_matrix = mathutils.Matrix.Scale(1.5, 4, (1, 0, 0))

transform_matrix = translation_matrix @ rotation_matrix @ scale_matrix
cube.matrix_world @= transform_matrix
```
Here, three transformation matrices are created using the `mathutils.Matrix` functions. The `translation_matrix` translates the cube by 2 units along the Z-axis, the `rotation_matrix` rotates the cube by `rotation_angle` around the X-axis, and the `scale_matrix` scales the cube by a factor of 1.5 along the X-axis. These matrices are then combined using the matrix multiplication operator `@` to create the `transform_matrix`. Finally, the `matrix_world` attribute of the cube object is updated by multiplying it with the `transform_matrix`, effectively applying the transformation to the cube.


-- Here are some resources I used to finish this section:

[Example Q1](https://drive.google.com/file/d/14tKop2gsH-qVmRg7ivnd9I-Gq1Y0A4WZ/view?usp=drive_link)

[Transformation](https://drive.google.com/file/d/1Yl3ivEIXf5Pf4apzrRMajkBhNnZYzusJ/view?usp=drive_link)

[Template](https://drive.google.com/file/d/1bJxdYUJspVPnGqMwwl5yK7Y00dLbSXRe/view?usp=drive_link)

[Shader Library](https://drive.google.com/file/d/1aTdW11C50MgvTcH25-QAfH7IA6RoMSj-/view?usp=drive_link)

[Untitled](https://drive.google.com/file/d/1w21yWIsuB6kTOtH2vFQB-zEVWlmgGcDf/view?usp=drive_link)



# ****Python & Docker****

Q2.1: Describe the steps to create a Docker container for a Python-based application. What information would you need to include in the Dockerfile?

`Answer:`To create a Docker container for a Python-based application, we can follow these steps:

**Creating a Dockerfile:** We can start by creating a file called `Dockerfile` in the root directory of our project. This file will contain instructions to build our Docker image.

**Specifying the base image:** In the Dockerfile, we can begin by specifying the base image we want to use. For a Python-based application, we can use an official Python base image. We have to choose an appropriate tag, such as `python:3.9`, to specify the Python version we need.
```javascript
# Using the official Python base image with Python 3.9
FROM python:3.9
```
**Copying the application code:** Next, copying the application code into the Docker image. This is typically done using the `COPY` instruction in the Dockerfile. Specifying the source directory of the code and the destination directory within the image.
```javascript
# Copying the application code into the container
COPY . /app
```
**Setting the working directory:** Using the `WORKDIR` instruction to set the working directory inside the image. This is the directory where subsequent commands will be executed.
```javascript
# Setting the working directory inside the container
WORKDIR /app
```
**Installing dependencies:** If our application has dependencies, we need to install them inside the Docker image. This can be done using the `RUN` instruction, which allows us to execute commands inside the image during the build process.
```javascript
# Installing dependencies
RUN pip install -r requirements.txt
```
**Expose any necessary ports:** If our application listens on a specific port, we need to expose that port to allow external access. Using the `EXPOSE` instruction to specify the desired port number.
```javascript
# Exposing port 5000 for the Flask application
EXPOSE 8080
```
**Define the startup command:** Finally, specifying the command that should be run when the container starts. This is done using the `CMD` instruction.
```javascript
# Defining the startup command
CMD ["python", "app.py"]
```
**Build the Docker image:** With the Dockerfile in place, we can now build the Docker image. we have to open a terminal or command prompt, navigate to the directory containing the Dockerfile, and run the following command:
```javascript
# Building the docker image
docker build -t myapp .
```
**Run the Docker container:** Once the image is built, we can run a container based on it. Use the following command to start a container from the image:
```javascript
docker run -p 8080:8080 myapp
```
This command maps port 8080 of the host machine to port 8080 inside the container, allowing you to access the application from your local machine.


In the Dockerfile, we would typically include the following information:

- **Base image:** We have to specify the base image that our Docker image will be built upon. This can be an official Python base image or any other image that suits our application's requirements.


- **Working directory:** Then we need to set the working directory inside the container where subsequent commands will be executed.


- **Copying files:** We have to copy our application code and any necessary files into the container. This ensures that the container has access to our code during runtime.


- **Installing dependencies:** If our application has any dependencies, we need to install them inside the container. This can be done using package managers like pip or conda.


- **Exposing ports:** If our application listens on a specific port, we should expose that port in the Dockerfile so that it can be accessed from outside the container.


- **Setting environment variables:** If our application requires any environment variables to run correctly, we can set them in the Dockerfile.


- **Defining the startup command:** Finally, we have to specify the command that should be executed when the container starts. This command typically runs our application.


Q2.2: Explain how you can use Docker Compose to manage multi-container Python applications.

`Answer:`Docker Compose is a tool that simplifies the management of multi-container Docker applications. It allows us to define and run multiple containers as a single service, making it easier to orchestrate complex applications. Here's an example of how to use Docker Compose to manage a multi-container Python application:

- **Install Docker Compose:** First, we have to ensure that we have Docker Compose installed on our system.

- **Creating a Docker Compose YAML file:** Then we have to create a file named `docker-compose.yml` in the root directory of our project. This file will contain the configuration for our multi-container application.

- **Defining services:** In the `docker-compose.yml` file, we have to specify the services (containers) that make up our application. Each service represents a separate container. In this example, let's consider a Python application with a web server and a PostgreSQL database.

Example `docker-compose.yml`:
```javascript
version: '3.9'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - db
  db:
    image: postgres
    environment:
      - POSTGRES_USER=myuser
      - POSTGRES_PASSWORD=mypassword
```
In this example, we define two services: `web` and `db`. The `web` service is built using the Dockerfile in the current directory (`build: .`). It maps port 5000 of the host machine to port 5000 of the container (`ports: - "5000:5000"`). It also specifies a dependency on the db service, which means that the db service will be started before the web service (`depends_on: - db`).

The `db` service uses the official PostgreSQL image (`image: postgres`). It sets the environment variables for the PostgreSQL container, including the username and password.

- **Building and running the containers:** Now, we have to open a terminal or command prompt, navigate to the directory containing the `docker-compose.yml` file, and run the following command:
```javascript
docker-compose up
```
This command will build the necessary Docker images and create and start the containers based on the configuration in the `docker-compose.yml` file. We should see the logs from both containers being displayed in the terminal.

- **Accessing the application:** Once the containers are up and running, we can access the web server from our browser by visiting http://localhost:5000. The web server container can communicate with the PostgreSQL database using the service name defined in the `docker-compose.yml` file (`db`).

- **Stopping the containers:** To stop the containers, we can press `Ctrl + C` in the terminal running the docker-compose up command. Alternatively, we can run the following command in a separate terminal:
```javascript
docker-compose down
```
This command will stop and remove the containers, but it will preserve the data stored in the PostgreSQL container because the data is stored in a Docker volume by default.

- **Exposing ports:** If our application listens on a specific port, we should expose that port in the Dockerfile so that it can be accessed from outside the container.


- **Setting environment variables:** If our application requires any environment variables to run correctly, we can set them in the Dockerfile.


- **Defining the startup command:** Finally, we have to specify the command that should be executed when the container starts. This command typically runs our application.

-- Here are some resources I used to finish this section:

[Script Docker](https://drive.google.com/drive/folders/1gUoHQh3HsOftifhJppGoTmzYq2wpYuPx?usp=drive_link)

[Hello Docker](https://drive.google.com/drive/folders/1-WLLqumygrbm2bTmWbBcP5LeUJBooS2c?usp=drive_link)

[Fastapi Docker](https://drive.google.com/drive/folders/1pk3Nq_mhDBeE43FBi_EOytDxCNG89gxX?usp=drive_link)

[Docker socket](https://drive.google.com/drive/folders/1v0a5hsidDEF0lMX6bQgLN9tVmxlXqsIq?usp=drive_link)

[Example yml](https://drive.google.com/drive/folders/1WIGm1TwWo6ZkbHT6vBYKvgcyO6wO8g35?usp=sharing)

[Word Press Site](https://drive.google.com/drive/folders/1vMCzWmgYTY1ObYbjHK0eJxXDee_h84QW?usp=sharing)



# ****JavaScript 3D (Three.js)****

Q3.1: Describe the fundamental components needed to render a basic 3D scene using Three.js.

`Answer`: To render a basic 3D scene using Three.js, we will need several fundamental components. Here's an overview of the key elements:

**Scene:** The Scene object serves as a container for all the 3D objects, lights, and cameras in our scene. It acts as a parent to all the objects we want to render.
```javascript
// Creating a scene
var scene = new THREE.Scene();
```
**Camera:** The Camera determines the perspective and view of our scene. Three.js provides various camera types, such as PerspectiveCamera or OrthographicCamera. The camera's position and orientation control what is visible in the rendered scene.
```javascript
// Creating a camera
var camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.z = 5;
```
**Renderer:** The Renderer is responsible for transforming the 3D objects and scene into the final 2D image that is displayed on the screen. Three.js provides WebGLRenderer, which uses WebGL to perform high-performance rendering.
```javascript
// Creating a renderer
var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
```
**Geometry:** The Geometry defines the shape and structure of 3D objects. Three.js includes several built-in geometries like BoxGeometry, SphereGeometry, and PlaneGeometry. We can also create custom geometries by specifying vertices and faces manually.
```javascript
// Creating a geometry (BoxGeometry)
var geometry = new THREE.BoxGeometry(1, 1, 1);
```
**Material:** The Material determines the appearance of a 3D object, such as its color, texture, transparency, and shading. Three.js provides a variety of material types like MeshBasicMaterial, MeshPhongMaterial, and MeshLambertMaterial, each with different properties and visual effects.
```javascript
// Creating a material (MeshBasicMaterial)
var material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
```
**Mesh:** The Mesh combines the geometry and material to create a visible 3D object. It represents a single instance of a geometric shape in the scene.
```javascript
// Creating a mesh by combining the geometry and material
var cube = new THREE.Mesh(geometry, material);
```
**Light:** The Light objects define the light sources that illuminate the scene and affect the appearance of objects. Three.js supports different light types, including AmbientLight, DirectionalLight, PointLight, and SpotLight.
```javascript
// Creating a light source (PointLight)
var light = new THREE.PointLight(0xffffff, 1);
light.position.set(2, 2, 2);
```
**Animation:** Three.js provides animation capabilities to bring our 3D scene to life. We can animate the position, rotation, scale, and other properties of objects using keyframes or tweening libraries like Tween.js.
```javascript
// Animation function
function animate() {
  requestAnimationFrame(animate);

  // Rotate the cube
  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;

  // Render the scene with the camera
  renderer.render(scene, camera);
}

// Call the animation function
animate();
```
These fundamental components work together to create a basic 3D scene in Three.js. By customizing and expanding upon these components, we can create complex and interactive 3D graphics in your web applications.


Q3.2: How can you import and use a 3D model created in Blender within a Three.js application?

`Answer`: To import and use a 3D model created in Blender within a Three.js application, we can follow these steps:

**Model Export from Blender:**

- Open the model in Blender.
- Ensure that the model is properly UV-mapped and textured.
- Export the model to a compatible format like `.glb` or `.gltf`. These formats store both the geometry and materials of the model.

**Importing Three.js Libraries:**
- Include the Three.js library in the HTML file by adding a script tag:
```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/0.132.2/three.min.js"></script>
```
- Optionally, include additional libraries like `OrbitControls` or `GLTFLoader` if needed.
**Setting up the Scene:**

- Create a scene, camera, and renderer as described in the previous examples.

**Loading and Displaying the Model:**
- Create a loader object to load the model file. In this example, we'll use `GLTFLoader` to load a `.glb` or `.gltf` file:
```javascript
var loader = new THREE.GLTFLoader();
```
- Load the model using the loader's `load` function:
```javascript
loader.load('path/to/model.glb', function (gltf) {
  // Callback function called after the model is loaded
  var model = gltf.scene;

  // Manipulate or position the model if needed
  // For example: model.position.set(x, y, z);

  // Add the model to the scene
  scene.add(model);
});
```
**Lighting and Rendering:**

- Add lights to the scene if necessary.
- Render the scene using the renderer as shown in the previous examples.

By following these steps, we can successfully import and use a 3D model created in Blender within a Three.js application.



-- Here are some resources I used to finish this section:

[Example](https://drive.google.com/drive/folders/1syUwjYP17OtNPQn6P0Tmjc4ZkLb0L7Ja?usp=drive_link)

[Threetut](https://drive.google.com/drive/folders/1TrefvIxIRAMyz4tlYIyuSI7JmM-Zy3qr?usp=drive_link)

[Blender_Threejs](https://drive.google.com/drive/folders/1AU6sM5klP0E6ipbxlUUgcV_9SgOvKgTP?usp=sharing)

