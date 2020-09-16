# Exercise-02c-Color-Maze

Select the Player node, and in the Inspector, go to PhysicsBody2D->Collision. Make sure the fourth square from the left (on the first row) is the only one highlighted.

Right-click on the Player node, and Attach Script. Create a new script (Player.gd) in the Player folder. Replace its contents with the following:

```
extends KinematicBody2D

var rot_amount = 1.5
var ready_to_shoot = true
onready var Ball = load("res://Ball/Ball.tscn")

func _physics_process(delta):
	if Input.is_action_pressed("left"):
		rotation_degrees -= rot_amount
	if Input.is_action_pressed("right"):
		rotation_degrees += rot_amount

	if Input.is_action_pressed("red"):
		shoot("red")
	if Input.is_action_pressed("yellow"):
		shoot("yellow")
	if Input.is_action_pressed("blue"):
		shoot("blue")


func shoot(color):
		if ready_to_shoot:
			var b = Ball.instance()
			b.color = color
			b.position = position
			b.position += Vector2(0, -40).rotated(rotation)
			get_parent().add_child(b)
			b.apply_central_impulse(Vector2(0,-100).rotated(rotation))
			ready_to_shoot = false
			$Reload.start()
```

Select the Reload node. In the Node panel (tab next to the Inspector panel), Signals, double-click on the timeout() signal. Connect it to the Player script (leave the Receiver Method `_on_Reload_timeout`) and then press Connect. You should now be brought back to the Player.gd script.

In the new `func _on_Reload_timeout():` method, add the following line:
```
func _on_Reload_timeout():
	ready_to_shoot = true
```

Test the game. You should be able to shoot red, yellow, or blue bullets that destroy the red, yellow, and blue tiles (respectively).

**Extra credit: how could you make this more like a real game? Make your additions, and describe them in the resulting README.md**

Quit Godot. In GitHub desktop, you should now see the updated files listed in the left panel. In the bottom of that panel, type a Summary message (something like "Completes the game development") and press the "Commit to master" button. On the right side of the top, black panel, you should see a button labeled "Push origin". Press that now.

If you return to and refresh your GitHub repository page, you should now see your updated files with the time when they were changed.

Now edit the README.md file. When you have finished editing, commit your changes, and then turn in the URL of the main repository page (https://github.com/[username]/Exercise-02c-Color-Maze) on Canvas.

The final state of the file should be as follows (replacing my information with yours):
```
# Exercise-02c-Color-Maze
Exercise for MSCH-C220, 15 September 2020

A simple game exploring physics bodies, collision layers, scenes, and signals

## Implementation
Built using Godot 3.2.2

## References
None

## Future Development
None

## Created by 
Jason Francis

```
