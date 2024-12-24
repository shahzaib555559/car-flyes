# car-flyes
best game i try to play its hard broooo
CarController.cs
using UnityEngine;

public class CarController : MonoBehaviour
{
    public float speed = 10f;             // Forward speed of the car
    public float turnSpeed = 200f;        // Turning speed of the car
    public float brakeForce = 50f;        // Braking force

    private float moveInput;              // Input for forward/backward
    private float turnInput;              // Input for turning

    private Rigidbody rb;                 // Rigidbody of the car

    void Start()
    {
        // Get the Rigidbody component
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Get the player's input
        moveInput = Input.GetAxis("Vertical");  // W/S or Arrow keys (forward/back)
        turnInput = Input.GetAxis("Horizontal"); // A/D or Arrow keys (left/right)

        // Apply movement and rotation
        MoveCar();
    }

    void MoveCar()
    {
        // Apply forward/backward movement
        Vector3 moveDirection = transform.forward * moveInput * speed * Time.deltaTime;
        rb.MovePosition(rb.position + moveDirection);

        // Apply turning
        float turn = turnInput * turnSpeed * Time.deltaTime;
        rb.MoveRotation(rb.rotation * Quaternion.Euler(0, turn, 0));
        
        // Optionally, apply brake force
        if (moveInput == 0)
        {
            rb.velocity = Vector3.Lerp(rb.velocity, Vector3.zero, brakeForce * Time.deltaTime);
        }
    }
}
Explanation of the Code:
Input: Input.GetAxis("Vertical") is used for forward and backward movement (W/S or Arrow keys), while Input.GetAxis("Horizontal") is used for turning the car left and right (A/D or Arrow keys).
Rigidbody: The script uses Unity's Rigidbody component to handle physics and movement.
Movement: The car moves based on input, and rotation is applied for turning.
Braking: When there’s no forward/backward input, the car will gradually slow down (braking effect).
5. Assign the Car Controller to the Car
In Unity’s Hierarchy window, select the car object.
In the Inspector window, click Add Component and attach the CarController script to your car.
You may need to adjust the car’s Rigidbody component (if it exists), ensuring that the mass, drag, and other properties are set correctly.
6. Camera Follow Script
To follow the car with the camera, add a simple follow script to the camera.

CameraFollow.cs
Create a new C# script and name it CameraFollow.
Attach it to the Main Camera in the scene.
csharp
Copy code
using UnityEngine;

public class CameraFollow : MonoBehaviour
{
    public Transform car;            // The car to follow
    public Vector3 offset = new Vector3(0, 5, -10); // Camera's relative position to the car
    public float smoothSpeed = 0.125f;  // Camera smoothing speed

    void Update()
    {
        // Smoothly move the camera towards the car
        Vector3 desiredPosition = car.position + offset;
        Vector3 smoothedPosition = Vector3.Lerp(transform.position, desiredPosition, smoothSpeed);
        transform.position = smoothedPosition;

        // Always look at the car
        transform.LookAt(car);
    }
}
using UnityEngine;
public class CarController : MonoBehaviour
{
    public float speed = 10f;             // Forward speed of the car
    public float turnSpeed = 200f;        // Turning speed of the car
    public float brakeForce = 50f;        // Braking force

    private float moveInput;              // Input for forward/backward
    private float turnInput;              // Input for turning

    private Rigidbody rb;                 // Rigidbody of the car

    void Start()
    {
        // Get the Rigidbody component
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Get the player's input
        moveInput = Input.GetAxis("Vertical");  // W/S or Arrow keys (forward/back)
        turnInput = Input.GetAxis("Horizontal"); // A/D or Arrow keys (left/right)

        // Apply movement and rotation
        MoveCar();
    }

    void MoveCar()
    {
        // Apply forward/backward movement
        Vector3 moveDirection = transform.forward * moveInput * speed * Time.deltaTime;
        rb.MovePosition(rb.position + moveDirection);

        // Apply turning
        float turn = turnInput * turnSpeed * Time.deltaTime;
        rb.MoveRotation(rb.rotation * Quaternion.Euler(0, turn, 0));
        
        // Optionally, apply brake force
        if (moveInput == 0)
        {
            rb.velocity = Vector3.Lerp(rb.velocity, Vector3.zero, brakeForce * Time.deltaTime);
        }
    }
}
Explanation of the Code:
Input: Input.GetAxis("Vertical") is used for forward and backward movement (W/S or Arrow keys), while Input.GetAxis("Horizontal") is used for turning the car left and right (A/D or Arrow keys).
Rigidbody: The script uses Unity's Rigidbody component to handle physics and movement.
Movement: The car moves based on input, and rotation is applied for turning.
Braking: When there’s no forward/backward input, the car will gradually slow down (braking effect).
5. Assign the Car Controller to the Car
In Unity’s Hierarchy window, select the car object.
In the Inspector window, click Add Component and attach the CarController script to your car.
You may need to adjust the car’s Rigidbody component (if it exists), ensuring that the mass, drag, and other properties are set correctly.
6. Camera Follow Script
To follow the car with the camera, add a simple follow script to the camera.

CameraFollow.cs
Create a new C# script and name it CameraFollow.
Attach it to the Main Camera in the scene.
csharp
Copy code
using UnityEngine;

public class CameraFollow : MonoBehaviour
{
    public Transform car;            // The car to follow
    public Vector3 offset = new Vector3(0, 5, -10); // Camera's relative position to the car
    public float smoothSpeed = 0.125f;  // Camera smoothing speed

    void Update()
    {
        // Smoothly move the camera towards the car
        Vector3 desiredPosition = car.position + offset;
        Vector3 smoothedPosition = Vector3.Lerp(transform.position, desiredPosition, smoothSpeed);
        transform.position = smoothedPosition;

        // Always look at the car
        transform.LookAt(car);
    }
}
