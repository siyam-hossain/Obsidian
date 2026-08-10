# Cube Design

##### Header files

It **imports the libraries/classes needed for your OpenGL program**.

```cpp
#include <glad/glad.h>
#include <GLFW/glfw3.h>

#include <glm/glm.hpp>
#include <glm/gtc/matrix_transform.hpp>
#include <glm/gtc/type_ptr.hpp>

#include "shader.h"
#include "basic_camera.h"
```

- `glad.h` → OpenGL functions
- `glfw3.h` → Window and input handling
- `glm.hpp` → Vectors and matrices
- `matrix_transform.hpp` → Translate, rotate, scale
- `type_ptr.hpp` → Connect GLM data with OpenGL
- `shader.h` → Your shader class
- `basic_camera.h` → Your camera class

---

##### drawCube()

This is the **function declaration** for `drawCube()`. It tells C++ what information the function needs:

```cpp
void drawCube(
	Shader shaderProgram,
	unsigned int VAO,
	glm::mat4 parentTrans,
	float posX = 0.0,
	float posY = 0.0,
	float posz = 0.0,
	float rotX = 0.0,
	float rotY = 0.0,
	float rotZ = 0.0,
	float scX = 1.0,
	float scY = 1.0,
	float scZ=1.0
);
```

- `Shader shaderProgram` → shader to use
- `unsigned int VAO` → cube's VAO
- `glm::mat4 parentTrans` → parent transformation
- `posX, posY, posz` → cube position
- `rotX, rotY, rotZ` → cube rotation
- `scX, scY, scZ` → cube scale

The `(= ...)` values are **default values**, used when you don't provide those arguments.

---

##### Window settings

```cpp
const unsigned int SCR_WIDTH = 800;
const unsigned int SCR_HEIGHT = 600;
```

They define the **window size**:

- `SCR_WIDTH` → width = **800 pixels**
- `SCR_HEIGHT` → height = **600 pixels**

`const` means their values **cannot be changed**.

---

##### Modeling Transformation initialization

```cpp
float rotateAngle_X = 45.0;
float rotateAngle_Y = 45.0;
float rotateAngle_Z = 45.0;

float rotateAxis_X = 0.0;
float rotateAxis_Y = 0.0;
float rotateAxis_Z = 1.0;
float translate_X = 0.0;
float translate_Y = 0.0;
float translate_Z = 0.0;

float scale_X = 1.0;
float scale_Y = 1.0;
float scale_Z = 1.0;
```

These variables control the cube's **transformation**:

- `rotateAngle_X/Y/Z` → rotation angle around X, Y, Z axes (**45°** each)
- `rotateAxis_X/Y/Z` → rotation axis (**Z-axis** here)
- `translate_X/Y/Z` → cube position (**0, 0, 0**)
- `scale_X/Y/Z` → cube size (**1, 1, 1**, original size)

---

##### Set initial mouse position

```cpp
float lastX = SCR_WIDTH / 2.0f;
float lastY = SCR_HEIGHT / 2.0f;
bool firstMouse = true;
```

- `lastX` → previous mouse **X position**, initially center (`400`)
- `lastY` → previous mouse **Y position**, initially center (`300`)
- `firstMouse` → checks whether this is the **first mouse movement**.
- It prevents a sudden jump when mouse movement starts.

It sets the **initial mouse position** to the center of the window.

For an `800 × 600` window:

- `lastX = 800 / 2 = 400`
- `lastY = 600 / 2 = 300`

So initially:
**`lastX = 400, lastY = 300`** → center of the window.

---

##### Camera setup

```cpp
float 	eyeX = 0.0,
		eyeY = 0.0,
		eyeZ = 3.0;

float 	lookAtX = 0.0,
		lookAtY = 0.0,
		lookAtZ = 0.0;

glm::vec3 V = glm::vec3(
	0.0f,
	1.0f,
	0.0f
);
```

These define the **camera setup**:

- `eyeX, eyeY, eyeZ` → camera position: **(0, 0, 3)**
- `lookAtX, lookAtY, lookAtZ` → where the camera looks: **(0, 0, 0)**
- `V` → camera's **up direction**: **(0, 1, 0)**, meaning Y-axis is up.

Note:
`eyeZ = 3.0` not indicate pixel rather it indicate it 3 unit far way from origin `(0, 0, 0)`

---

##### BasicCamera object

It **creates a `BasicCamera` object** using the camera settings:

```cpp
BasicCamera basic_camera(
    eyeX, eyeY, eyeZ,          // camera position
    lookAtX, lookAtY, lookAtZ, // looking toward
    V                         // up direction
);
```

So `basic_camera` now stores the **camera position, viewing direction, and up direction**.

---

##### Measure time between frames

They are used to **measure time between frames**.

```cpp
float deltaTime = 0.0f;
float lastFrame = 0.0f;
```

- `lastFrame` → stores the time of the **previous frame**
- `deltaTime` → stores the **time difference between the current and previous frame**

This helps make movement/animation **independent of FPS**.

---

##### Depth Testing

```cpp
glEnable(GL_DEPTH_TEST);
```

It **enables depth testing** in OpenGL.
This makes OpenGL correctly decide **which 3D object is in front of another**.
Without it, objects may appear drawn in the wrong order.

---

##### Shader Objects

These lines **create two `Shader` objects**:

```cpp
Shader ourShader("vertexShader.vs", "fragmentShader.fs");
```

Uses:

- `vertexShader.vs` → vertex shader
- `fragmentShader.fs` → fragment shader

```cpp
Shader constantShader("vertexShader.vs", "fragmentShaderV2.fs");
```

Uses:

- `vertexShader.vs` → same vertex shader
- `fragmentShaderV2.fs` → different fragment shader

So, both shaders use the **same vertex processing**, but have **different fragment/color processing**.

---

##### Cube vertex data

```cpp
    float cube_vertices[] = {
        0.0f, 0.0f, 0.0f, 0.3f, 0.8f, 0.5f,
        0.5f, 0.0f, 0.0f, 0.5f, 0.4f, 0.3f,
        0.5f, 0.5f, 0.0f, 0.2f, 0.7f, 0.3f,
        0.0f, 0.5f, 0.0f, 0.6f, 0.2f, 0.8f,
        0.0f, 0.0f, 0.5f, 0.8f, 0.3f, 0.6f,
        0.5f, 0.0f, 0.5f, 0.4f, 0.4f, 0.8f,
        0.5f, 0.5f, 0.5f, 0.2f, 0.3f, 0.6f,
        0.0f, 0.5f, 0.5f, 0.7f, 0.5f, 0.4f
    };
```

```text
(0,0,0)
(0.5,0,0)
(0.5,0.5,0)
(0,0.5,0)
(0,0,0.5)
(0.5,0,0.5)
(0.5,0.5,0.5)
(0,0.5,0.5)
```

This array stores the **cube's vertex data**.

Each vertex has **6 values**:

```text
X, Y, Z,   R, G, B
```

For example:

```cpp
0.0f, 0.0f, 0.0f,   0.3f, 0.8f, 0.5f
```

means:

- `(0.0, 0.0, 0.0)` → vertex position
- `(0.3, 0.8, 0.5)` → vertex color

There are **8 vertices**, which define the corners of the cube.

---

##### Cube's triangles

```cpp
unsigned int cube_indices[] = {
   0, 3, 2,
   2, 1, 0,

   1, 2, 6,
   6, 5, 1,

   5, 6, 7,
   7 ,4, 5,

   4, 7, 3,
   3, 0, 4,

   6, 2, 3,
   3, 7, 6,

   1, 5, 4,
   4, 0, 1
};
```

This array stores the **indices that tell OpenGL how to form the cube's triangles**.

Each **3 numbers = 1 triangle**:

```text
0, 3, 2  → triangle 1
2, 1, 0  → triangle 2
```

Together, those 2 triangles form **one square face** of the cube.

- Since a cube has **6 faces**:
- **6 faces × 2 triangles = 12 triangles**
- So there are **36 indices** in total.

---

##### Creates three OpenGL object IDs

```cpp
unsigned int VBO, VAO, EBO;
```

Creates three **OpenGL object IDs**:

- `VAO` → stores vertex configuration
- `VBO` → stores vertex data
- `EBO` → stores index data

```cpp
glGenVertexArrays(1, &VAO);
glGenBuffers(1, &VBO);
glGenBuffers(1, &EBO);
```

These functions ask OpenGL to **create/generate those objects** and give each one an ID.

---

##### Position data from each vertex

This tells OpenGL **how to read the position data from each vertex**.

```cpp
glVertexAttribPointer(
    0,                  // attribute location
    3,                  // 3 values: X, Y, Z
    GL_FLOAT,           // data type
    GL_FALSE,
    6 * sizeof(float),  // distance to next vertex (6 x 4 = 24 bytes)
    (void*)0            // position starts at beginning (offset)
);
```

Because each vertex is:

```text
X Y Z R G B
```

the position is the **first 3 floats**.

```cpp
glEnableVertexAttribArray(0);
```

→ Enables vertex attribute **0**, so the shader can use the position data.

---

##### Color data from each vertex

This tells OpenGL **how to read the color data** from each vertex.

```cpp
glVertexAttribPointer(
    1,                  // attribute location
    3,                  // R, G, B
    GL_FLOAT,           // data type
    GL_FALSE,
    6 * sizeof(float),  // next vertex is 6 floats away
    (void*)12           // color starts after 3 floats (offset 12 bytes, or 4th value)
);
```

Since each vertex is:

```text
X Y Z | R G B
```

`(void*)12` means **skip the first 3 floats (12 bytes)** and start reading the color.

```cpp
glEnableVertexAttribArray(1);
```

→ Enables vertex attribute **1** for the color.

---

##### Background color of the OpenGL window

```cpp
glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
```

Sets the **background color** of the OpenGL window.

```text
0.2 → Red
0.3 → Green
0.3 → Blue
1.0 → Alpha (fully opaque)
```

The color is applied when you call:

```cpp
glClear(GL_COLOR_BUFFER_BIT);
```

---

##### Projection Matrix

This creates a **projection matrix** for the camera:

```cpp
glm::mat4 projection = glm::perspective(
    glm::radians(basic_camera.Zoom), // field of view
    (float)SCR_WIDTH / SCR_HEIGHT,    // aspect ratio
    0.1f,                             // near limit
    100.0f                            // far limit
);
```

It determines **how the 3D scene is projected onto the 2D screen**.

- `Zoom` → how wide/narrow the camera view is
- `800 / 600` → screen aspect ratio
- `0.1` → closest visible distance
- `100` → farthest visible distance

---

##### Projection matrix

It **sends the projection matrix to the shaders**.

```cpp
ourShader.setMat4("projection", projection);
constantShader.setMat4("projection", projection);
```

- `"projection"` → name of the matrix variable in the shader.
- `projection` → the matrix you created.
- Both shaders receive the **same projection matrix**.

---

##### Model transformation

```cpp
// Modelling Transformation
glm::mat4 identityMatrix = glm::mat4(1.0f);
// make sure to initialize matrix to identity matrix first

drawCube(
	ourShader,
	VAO,
	identityMatrix,
	translate_X,
	translate_Y,
	translate_Z,
	rotateAngle_X,
	rotateAngle_Y,
	rotateAngle_Z,
	scale_X,
	scale_Y,
	scale_Z
);
```

This creates the **model transformation** and draws the cube.

```cpp
glm::mat4 identityMatrix = glm::mat4(1.0f);
```

Creates an **identity matrix** as the starting point.

Then:

```cpp
drawCube(...)
```

passes the cube's:

- position → `translate_X/Y/Z`
- rotation → `rotateAngle_X/Y/Z`
- scale → `scale_X/Y/Z`

to `drawCube()`, which uses them to create the cube's **final model transformation**.

---

##### processInput()

```cpp
void processInput(GLFWwindow* window)
{
    if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
        glfwSetWindowShouldClose(window, true);

    if (glfwGetKey(window, GLFW_KEY_I) == GLFW_PRESS) translate_Y += 0.01;
    if (glfwGetKey(window, GLFW_KEY_K) == GLFW_PRESS) translate_Y -= 0.01;
    if (glfwGetKey(window, GLFW_KEY_L) == GLFW_PRESS) translate_X += 0.01;
    if (glfwGetKey(window, GLFW_KEY_J) == GLFW_PRESS) translate_X -= 0.01;
    if (glfwGetKey(window, GLFW_KEY_O) == GLFW_PRESS) translate_Z += 0.01;
    if (glfwGetKey(window, GLFW_KEY_P) == GLFW_PRESS) translate_Z -= 0.01;

    if (glfwGetKey(window, GLFW_KEY_X) == GLFW_PRESS)
    {
        rotateAngle_X += 1;
    }
    if (glfwGetKey(window, GLFW_KEY_Y) == GLFW_PRESS)
    {
        rotateAngle_Y += 1;
    }
    if (glfwGetKey(window, GLFW_KEY_Z) == GLFW_PRESS)
    {
        rotateAngle_Z += 1;
    }
}
```

This function **handles keyboard input to move and rotate the cube**.

- `ESC` → closes the window
- `I / K` → move cube **up / down** (`Y`)
- `L / J` → move cube **right / left** (`X`)
- `O / P` → move cube **forward / backward** (`Z`)
- `X` → rotate around **X-axis**
- `Y` → rotate around **Y-axis**
- `Z` → rotate around **Z-axis**

For example:

```cpp
if (glfwGetKey(window, GLFW_KEY_I) == GLFW_PRESS)
    translate_Y += 0.01;
```

While **I is held**, the cube moves upward by `0.01` world units each frame.

---

##### Draw cube and Transformation

```cpp
void drawCube(
	Shader shaderProgram,
	unsigned int VAO,
	glm::mat4 parentTrans,
	float posX,
	float posY,
	float posZ,
	float rotX,
	float rotY,
	float rotZ,
	float scX,
	float scY,
	float scZ
)
{
    shaderProgram.use();

    glm::mat4 translateMatrix, rotateXMatrix, rotateYMatrix, rotateZMatrix, scaleMatrix, model, modelCentered;

    //translation
    translateMatrix = glm::translate(
        parentTrans,
        glm::vec3(posX, posY, posZ)
    );

    //rotation
    rotateXMatrix = glm::rotate(
        translateMatrix,
        glm::radians(rotX),
        glm::vec3(1.0f, 0.0f, 0.0f)
    );
    rotateYMatrix = glm::rotate(
        rotateXMatrix,
        glm::radians(rotY),
        glm::vec3(0.0f, 1.0f, 0.0f)
    );
    rotateZMatrix = glm::rotate(
        rotateYMatrix,
        glm::radians(rotZ),
        glm::vec3(0.0f, 0.0f, 1.0f)
    );

	//scalling
    model = glm::scale(rotateZMatrix, glm::vec3(scX, scY, scZ));
    modelCentered = glm::translate(
        model,
        glm::vec3(-0.25, -0.25, -0.25)
    );

    shaderProgram.setMat4("model", modelCentered);

    glBindVertexArray(VAO);
    glDrawElements(GL_TRIANGLES, 36, GL_UNSIGNED_INT, 0);
}
```

This function **builds the cube's model matrix and then draws the cube**.

##### 1. Use the shader

```cpp
shaderProgram.use();
```

Activates the shader.

##### 2. Translation

```cpp
translateMatrix = glm::translate(
    parentTrans,
    glm::vec3(posX, posY, posZ)
);
```

Moves the cube to `(posX, posY, posZ)`.

##### 3. Rotation

```cpp
rotateXMatrix = glm::rotate(...);
rotateYMatrix = glm::rotate(...);
rotateZMatrix = glm::rotate(...);
```

Rotates the cube around **X → Y → Z** axes.

##### 4. Scaling

```cpp
model = glm::scale(
    rotateZMatrix,
    glm::vec3(scX, scY, scZ)
);
```

Changes the cube's size.

##### 5. Center the cube

```cpp
modelCentered = glm::translate(
    model,
    glm::vec3(-0.25, -0.25, -0.25)
);
```

Moves the cube's origin to its **center**.

##### 6. Send transformation to shader

```cpp
shaderProgram.setMat4("model", modelCentered);
```

Sends the final model matrix to the shader.

##### 7. Draw

```cpp
glBindVertexArray(VAO);
glDrawElements(GL_TRIANGLES, 36, GL_UNSIGNED_INT, 0);
```

Uses the cube's VAO and draws **36 indices = 12 triangles = 6 faces**.
