```cpp
#include <glad/glad.h>
#include <GLFW/glfw3.h>

#include <glm/glm.hpp>
#include <glm/gtc/matrix_transform.hpp>
#include <glm/gtc/type_ptr.hpp>

#include "shader.h"
#include "basic_camera.h"

#include <iostream>

using namespace std;

void framebuffer_size_callback(GLFWwindow *window, int width, int height);
void mouse_callback(GLFWwindow *window, double xpos, double ypos);
void scroll_callback(GLFWwindow *window, double xoffset, double yoffset);
void processInput(GLFWwindow *window);

// draw object functions
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
	float scZ = 1.0
);

// settings
const unsigned int SCR_WIDTH = 800;
const unsigned int SCR_HEIGHT = 600;

// modelling transform
float rotateAngle_X = 0.0;
float rotateAngle_Y = 0.0;
float rotateAngle_Z = 0.0;
float rotateAxis_X = 0.0;
float rotateAxis_Y = 0.0;
float rotateAxis_Z = 1.0;
float translate_X = 0.0;
float translate_Y = 0.0;
float translate_Z = 0.0;
float scale_X = 1.0;
float scale_Y = 1.0;
float scale_Z = 1.0;

// camera
float lastX = SCR_WIDTH / 2.0f;
float lastY = SCR_HEIGHT / 2.0f;
bool firstMouse = true;

float 	eyeX = 1.5, 
		eyeY = 1.5, 
		eyeZ = 3.0;
		
float 	lookAtX = 0.0, 
		lookAtY = 0.0, 
		lookAtZ = 0.0;

glm::vec3 V = glm::vec3(0.0f, 1.0f, 0.0f);

BasicCamera basic_camera(
	eyeX, 
	eyeY, 
	eyeZ, 
	lookAtX, 
	lookAtY, 
	lookAtZ, 
	V
);

// timing
float deltaTime = 0.0f; 
float lastFrame = 0.0f;

int main()
{
    // glfw: initialize and configure
    // ------------------------------
    glfwInit();
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

#ifdef __APPLE__
    glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);
#endif

    // glfw window creation
    // --------------------
    GLFWwindow *window = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "CSE 4208: Computer Graphics Laboratory", NULL, NULL);
    if (window == NULL)
    {
        std::cout << "Failed to create GLFW window" << std::endl;
        glfwTerminate();
        return -1;
    }
    glfwMakeContextCurrent(window);
    glfwSetFramebufferSizeCallback(window, framebuffer_size_callback);
    glfwSetCursorPosCallback(window, mouse_callback);
    glfwSetScrollCallback(window, scroll_callback);

    // tell GLFW to capture our mouse
    // glfwSetInputMode(window, GLFW_CURSOR, GLFW_CURSOR_DISABLED);

    // glad: load all OpenGL function pointers
    // ---------------------------------------
    if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress))
    {
        std::cout << "Failed to initialize GLAD" << std::endl;
        return -1;
    }

    // configure global opengl state
    // -----------------------------
    glEnable(GL_DEPTH_TEST);

    // build and compile our shader zprogram
    // ------------------------------------
    Shader ourShader("vertexShader.vs", "fragmentShader.fs");

    Shader constantShader("vertexShader.vs", "fragmentShaderV2.fs");

    // set up vertex data (and buffer(s)) and configure vertex attributes
    // ------------------------------------------------------------------
    float cube_vertices[] = {
        0.0f, 0.0f, 0.0f, 0.3f, 0.8f, 1.0f,
        1.0f, 0.0f, 0.0f, 0.5f, 0.4f, 0.3f,
        1.0f, 1.0f, 0.0f, 0.2f, 0.7f, 0.3f,
        0.0f, 1.0f, 0.0f, 0.6f, 0.2f, 0.8f,
        0.0f, 0.0f, 1.0f, 0.8f, 0.3f, 0.6f,
        1.0f, 0.0f, 1.0f, 0.4f, 0.4f, 0.8f,
        1.0f, 1.0f, 1.0f, 0.2f, 0.3f, 0.6f,
        0.0f, 1.0f, 1.0f, 0.7f, 1.0f, 0.4f};
    unsigned int cube_indices[] = {
        0, 3, 2,
        2, 1, 0,

        1, 2, 6,
        6, 5, 1,

        5, 6, 7,
        7, 4, 5,

        4, 7, 3,
        3, 0, 4,

        6, 2, 3,
        3, 7, 6,

        1, 5, 4,
        4, 0, 1};

    unsigned int VBO, VAO, EBO;
    glGenVertexArrays(1, &VAO);
    glGenBuffers(1, &VBO);
    glGenBuffers(1, &EBO);

    glBindVertexArray(VAO);

    glBindBuffer(GL_ARRAY_BUFFER, VBO);
    glBufferData(GL_ARRAY_BUFFER, sizeof(cube_vertices), cube_vertices, GL_STATIC_DRAW);

    glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);
    glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(cube_indices), cube_indices, GL_STATIC_DRAW);

    // position attribute
    glVertexAttribPointer(
		0, 
		3, 
		GL_FLOAT, GL_FALSE, 
		6 * sizeof(float), 
		(void *)0
	);
    glEnableVertexAttribArray(0);

    // color attribute
    glVertexAttribPointer(
		1, 
		3, 
		GL_FLOAT, 
		GL_FALSE, 
		6 * sizeof(float), 
		(void *)12
	);
    glEnableVertexAttribArray(1);

    // glPolygonMode(GL_FRONT_AND_BACK, GL_LINE);

    ourShader.use();
    // constantShader.use();

    // render loop
    // -----------
    while (!glfwWindowShouldClose(window))
    {
        // per-frame time logic
        // --------------------
        float currentFrame = static_cast<float>(glfwGetTime());
        deltaTime = currentFrame - lastFrame;
        lastFrame = currentFrame;

        // input
        // -----
        processInput(window);

        // render
        // ------
        glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

        // pass projection matrix to shader (note that in this case it could change every frame)
        glm::mat4 projection = glm::perspective(
			glm::radians(basic_camera.Zoom), 
			(float)SCR_WIDTH / (float)SCR_HEIGHT, 
			0.1f, 
			100.0f
		);
        // glm::mat4 projection = glm::ortho(-2.0f, +2.0f, -1.5f, +1.5f, 0.1f, 100.0f);
        ourShader.setMat4("projection", projection);
        constantShader.setMat4("projection", projection);

        // camera/view transformation
        glm::mat4 view = basic_camera.createViewMatrix();
        ourShader.setMat4("view", view);
        constantShader.setMat4("view", view);

        // Modelling Transformation
        glm::mat4 identityMatrix = glm::mat4(1.0f); 

        // paya
        drawCube(ourShader, VAO, identityMatrix, -0.4, 0.0, 0.4, 0.0, 0.0, 0.0, 0.1, 0.8, 0.1);
        drawCube(ourShader, VAO, identityMatrix, 0.4, 0.0, 0.4, 0.0, 0.0, 0.0, 0.1, 0.8, 0.1);
        drawCube(ourShader, VAO, identityMatrix, -0.4, 0.0, -0.4, 0.0, 0.0, 0.0, 0.1, 0.8, 0.1);
        drawCube(ourShader, VAO, identityMatrix, 0.4, 0.0, -0.4, 0.0, 0.0, 0.0, 0.1, 0.8, 0.1);

        // seat
        drawCube(ourShader, VAO, identityMatrix, 0.0, 0.45, 0.0, 0.0, 0.0, 0.0, 1.0, 0.1, 1.0);

        // back
        drawCube(ourShader, VAO, identityMatrix, 0.0, 0.90, -0.45, 0.0, 0.0, 0.0, 0.9, 0.8, 0.1);

        // render boxes
        // for (unsigned int i = 0; i < 10; i++)
        //{
        //    // calculate the model matrix for each object and pass it to shader before drawing
        //    glm::mat4 model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        //    model = glm::translate(model, cubePositions[i]);
        //    float angle = 20.0f * i;
        //    model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        //    drawCube(ourShader, VAO, model);
        //}

        // glfw: swap buffers and poll IO events (keys pressed/released, mouse moved etc.)
        // -------------------------------------------------------------------------------
        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    // optional: de-allocate all resources once they've outlived their purpose:
    // ------------------------------------------------------------------------
    glDeleteVertexArrays(1, &VAO);
    glDeleteBuffers(1, &VBO);
    glDeleteBuffers(1, &EBO);

    // glfw: terminate, clearing all previously allocated GLFW resources.
    // ------------------------------------------------------------------
    glfwTerminate();
    return 0;
}

// process all input: query GLFW whether relevant keys are pressed/released this frame and react accordingly
// ---------------------------------------------------------------------------------------------------------
void processInput(GLFWwindow *window)
{
    if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
        glfwSetWindowShouldClose(window, true);

    if (glfwGetKey(window, GLFW_KEY_I) == GLFW_PRESS)
        translate_Y += 0.01;
    if (glfwGetKey(window, GLFW_KEY_K) == GLFW_PRESS)
        translate_Y -= 0.01;
    if (glfwGetKey(window, GLFW_KEY_L) == GLFW_PRESS)
        translate_X += 0.01;
    if (glfwGetKey(window, GLFW_KEY_J) == GLFW_PRESS)
        translate_X -= 0.01;
    if (glfwGetKey(window, GLFW_KEY_O) == GLFW_PRESS)
        translate_Z += 0.01;
    if (glfwGetKey(window, GLFW_KEY_P) == GLFW_PRESS)
        translate_Z -= 0.01;

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

// glfw: whenever the window size changed (by OS or user resize) this callback function executes
// ---------------------------------------------------------------------------------------------
void framebuffer_size_callback(GLFWwindow *window, int width, int height)
{
    // make sure the viewport matches the new window dimensions; note that width and
    // height will be significantly larger than specified on retina displays.
    glViewport(0, 0, width, height);
}

// glfw: whenever the mouse moves, this callback is called, do as you please with it
// -------------------------------------------------------
void mouse_callback(GLFWwindow *window, double xposIn, double yposIn)
{
    // Rotate only while holding the left mouse button
    if (glfwGetMouseButton(window, GLFW_MOUSE_BUTTON_LEFT) != GLFW_PRESS)
    {
        firstMouse = true;
        return;
    }

    float xpos = static_cast<float>(xposIn);
    float ypos = static_cast<float>(yposIn);

    if (firstMouse)
    {
        lastX = xpos;
        lastY = ypos;
        firstMouse = false;
        return;
    }

    float xoffset = xpos - lastX;
    float yoffset = ypos - lastY;

    lastX = xpos;
    lastY = ypos;

    const float mouseSensitivity = 0.3f;

    rotateAngle_Y += xoffset * mouseSensitivity;
    rotateAngle_X += yoffset * mouseSensitivity;
}
// glfw: whenever the mouse scroll wheel scrolls, this callback is called
// ----------------------------------------------------------------------
void scroll_callback(GLFWwindow *window, double xoffset, double yoffset)
{
    basic_camera.ProcessMouseScroll(static_cast<float>(yoffset));
}


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
    translateMatrix = glm::translate(
		parentTrans, 
		glm::vec3(posX, posY, posZ)
	);
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
    model = glm::scale(
		rotateZMatrix, 
		glm::vec3(scX, scY, scZ)
	);
    modelCentered = glm::translate(
		model, 
		glm::vec3(-0.5, -0.5, -0.5)
	);

    shaderProgram.setMat4("model", modelCentered);

    glBindVertexArray(VAO);
    glDrawElements(GL_TRIANGLES, 36, GL_UNSIGNED_INT, 0);
}
```