---
tags:
  - note
  - bevy/0_15
Project:
  - "[[Map out useful bevy features]]"
Status: Finished
---
## Required components
### Summary 
A much more ergonomic way of creating bundles. In general bundles are being outmoded for required components. 

### Example
```rust
#[derive(Component, Default)]
#[require(Team, Sprite)]
struct Player {
    name: String,
}
```
What this basically means is that when I create a player it needs to be created alongside its required components. If these required components implement default they also get filled in without needing to do the below. 
```rust
commands.spawn(PlayerBundle {
    player: Player { 
        name: "hello".into(),
        ..default()
    },
    team: Team::Blue,
    ..default()
});
```
## Animation events
### Summary 
A way of tying an animation to an in-game event. The example provided is when a models foot hits the ground the dust cloud animation plays at that location. 

### Example
```rust
#[derive(Event, Clone)]
struct PlaySound {
    sound: Handle<AudioSource>,
}

// This will trigger the PlaySound event at the 1.5 second mark in `animation_clip`
animation_clip.add_event(1.5, PlaySound {
    sound: assets.load("sound.mp3"),
});

app.add_observer(|trigger: Trigger<PlaySound>, mut commands: Commands| {
    let sound = trigger.event().sound.clone();
    commands.spawn(AudioPlayer::new(sound));
});
```

## Gamepads as entities
### Summary 
They have made handling button inputs far simpler. 
### Example
#### New
```rust
fn gamepad_system(gamepads: Query<&Gamepad>) {
    for gamepad in &gamepads {
        if gamepad.just_pressed(GamepadButton::South) {
            println!("just pressed South");
        }

        let right_trigger = gamepad.get(GamepadButton::RightTrigger2).unwrap();
        if right_trigger.abs() > 0.01 {
            info!("RightTrigger2 value is {}", right_trigger);
        }

        let left_stick_x = gamepad.get(GamepadAxis::LeftStickX).unwrap();
        if left_stick_x.abs() > 0.01 {
            info!("LeftStickX value is {}", left_stick_x);
        }
    }
}
```

#### Old
```rust
fn gamepad_system(
   gamepads: Res<Gamepads>,
   button_inputs: Res<ButtonInput<GamepadButton>>,
   button_axes: Res<Axis<GamepadButton>>,
   axes: Res<Axis<GamepadAxis>>,
) {
    for gamepad in &gamepads {
        if button_inputs.just_pressed(
            GamepadButton::new(gamepad, GamepadButtonType::South)
        ) {
            info!("just pressed South");
        }

        let right_trigger = button_axes
           .get(GamepadButton::new(
               gamepad,
               GamepadButtonType::RightTrigger2,
           ))
           .unwrap();
        if right_trigger.abs() > 0.01 {
            info!("RightTrigger2 value is {}", right_trigger);
        }

        let left_stick_x = axes
           .get(GamepadAxis::new(gamepad, GamepadAxisType::LeftStickX))
           .unwrap();
        if left_stick_x.abs() > 0.01 {
            info!("LeftStickX value is {}", left_stick_x);
        }
    }
}
```

## Common Easing functions
### Summary 
Bevy now has some inbuilt common curves that can be used for a variety of things. 

### Example
```rust
// Ease between no rotation and a rotation of angle PI/2 about the y-axis.
let rotation_curve = EasingCurve::new(
    Quat::IDENTITY,
    Quat::from_rotation_y(FRAC_PI_2),
    EaseFunction::ElasticInOut,
)
.reparametrize_linear(interval(0.0, 4.0).unwrap())
.unwrap();
```