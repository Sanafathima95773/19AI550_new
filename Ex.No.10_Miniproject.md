# Ex.No: 10  Implementation of 2D/3D game 

### DATE: 23.05.2026                                                                    
### REGISTER NUMBER : 212223240145

### AIM: 

To develop a red ball inspired game in Unity 

### Algorithm:
```
1.Setup the Scene
Open Unity and create a 3D scene. Add a Sphere (rename to RedBall), Cubes (rename to Spikes), and Spheres (rename to Coins).

2.Add Physics Components
Attach a Rigidbody to the RedBall for physics interactions. Add Box Colliders to Spikes and Coins.

3.Create the Script
Create a C# Script → Name it RedBallController.cs. Write code for movement (forward/backward/jump) using Rigidbody.AddForce() or Transform.Translate().

4.Save and Attach the Script
Save the script and attach it to the RedBall GameObject. Ensure the RedBall has a Sphere Collider.

5.Configure Inputs
In the script, set up input axes (e.g., Input.GetAxis("Horizontal"), Input.GetKey(KeyCode.Space) for jumping).

6.Set Up the Coin Counter
Create a UI Text element in the Canvas to display the coin count. Use a GameManager script to track and update the score when the RedBall collides with Coins.

7.Test and Run
Press Play  in Unity to test the movement, collisions, and coin collection. Stop the program to make adjustments if needed.

```  
### Program:

*PlayerScript*

```
using UnityEngine;
using UnityEngine.UI;
using TMPro;
public class Playerscript: MonoBehaviour
{
    public float moveSpeed = 7f;
    public float jumpForce = 12f;

    Rigidbody2D rb;
    bool isGrounded = false;
    int coinCount = 0;

    public TMP_Text coinText; 

    void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        float h = Input.GetAxis("Horizontal");
        rb.linearVelocity = new Vector2(h * moveSpeed, rb.linearVelocity.y);

        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            rb.linearVelocity = new Vector2(rb.linearVelocity.x, jumpForce);
        }
    }

    void OnCollisionEnter2D(Collision2D col)
    {
        if (col.contacts[0].normal.y > 0.5f)
            isGrounded = true;
    }

    void OnCollisionExit2D(Collision2D col)
    {
        isGrounded = false;
    }

    void OnTriggerEnter2D(Collider2D col)
    {
        if (col.CompareTag("Coin"))
        {
            coinCount++;
            if (coinText != null)
                coinText.text = "Coins: " + coinCount;
            Destroy(col.gameObject);   // coin disappears
        }
    }
}
```

*CameraScript*

```
using UnityEngine;

public class Camerascript : MonoBehaviour
{
    public Transform target;       
    public float smoothSpeed = 5f;
    public Vector3 offset = new Vector3(0f, 1f, -10f);

    void LateUpdate()
    {
        if (target == null) return;

        Vector3 desired = target.position + offset;
        transform.position = Vector3.Lerp(
            transform.position, desired, smoothSpeed * Time.deltaTime);
    }
}
```
### Output:
<img width="1895" height="1010" alt="image" src="https://github.com/user-attachments/assets/ea4b783e-a77e-4212-b8fa-a8f1665bc56d" />

<img width="1485" height="997" alt="image" src="https://github.com/user-attachments/assets/5dc7e6d2-2c3e-40a2-9aff-37f6e371457c" />

<img width="1498" height="977" alt="image" src="https://github.com/user-attachments/assets/2f2c6554-1152-4a89-a2b3-c064932d1dc4" />

<img width="996" height="973" alt="image" src="https://github.com/user-attachments/assets/987954ff-ee65-4e0c-8389-cc40f8b59b58" />


### Result:
Thus the game was developed using Unity and adopted procedural generation AI technology.
