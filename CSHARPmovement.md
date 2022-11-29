# Unity-C-Sharp-Scripts-3D-MODEL
Scripts I used for my 3D video game character project in Unity. Allows for CharacterController, camera classes, and movement speed. 

# Movement.cs

using System.Collections;
using System.Collections.Generic;
using System.Data;
using UnityEngine;

public class Movement : MonoBehavior
{ 
  public CharacterController controller;
  
  public Transform cam;
  
  //public Animator animator;
  
  public float turnSmoothTime = 0.1f
  
  float turnSmoothVelocity;
  
  void Update()
  {
    float horizontal = Input.GetAxisRaw("Horizontal");
    float Vertical = Input.GetAxisRaw("Vertical");
    Vector3 direction = new Vector3(horizontal, 0f, vertical).normalized;
    
    if(direction.magnitude >= 0.1f)
    {
      float targetAngle = Mathf.Atan2(direction.x, direction.z) * Mathf.Rad2Deg * cam.eulerAngles-y;
      float angle = Mathf.SmoothDampAngle(transform.eulerAnglese.y, targetAngle, ref turnSmoothVelocity, turnSmoothTime);
      transform.rotation = Quaternion.Euler(0f, targetAngle, 0f);
      
      Vector3 moveDir = Quaternion.Euler(0f, targetAngle, 0f) * Vector3.forward;
      controller.Move(moveDir.normalized * speed * Time.deltaTime)
      //animator.SetBool("isWalking", vertical != 1 || horizontal != 1);
     }
    }
   }
  
