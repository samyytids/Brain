---
tags:
  - note
  - "#bevy/0_13"
Project:
  - "[[Map out useful bevy features]]"
Status: Finished
---
## Primitive shapes
### Summary 
Useful for rendering simple shapes

## Aabb2d / Bounding Circle
### Summary 
Handles collision detection based on parameters. These can be set up manually or form primitive shapes. 
You can check intersections between aab2d and bounding circles using the intersects method. 
These also interact with ray casting. 

### Example 
#### Aabb2d
```rust
let position = Vec2::new(100., 50.);
let half_size = Vec2::splat(20.);
let aabb = Aabb2d::new(position, half_size);
```

#### Bounding circle
```rust
let position = Vec2::new(80., 60.);
let radius = 30.;
let bounding_circle = BoundingCircle::new(postition, radius);
```

## System stepping
### Summary 
These are useful for handling debugging, using the egui you can have these run systems one step at a time so you can visually inspect potential bugs. 

## Slice scaling
### Summary 
Imagine you have a square with corners that contain detail. 
You want to stretch out the square without stretching the corner details. This lets you set areas that shouldn't be scaled and areas that should. 
Think of it as being a great way to scale UI elements. 

### Example
```rust
commands.spawn((
    SpriteSheetBundle::default(),
    ImageScaleMode::Sliced(TextureSlicer {
        // The image borders are 20 pixels in every direction
        border: BorderRect::square(20.0),
        // we don't stretch the corners more than their actual size (20px)
        max_corner_scale: 1.0,
        ..default()
    }),
));
```

## Tile scaling
### Summary 
Instead of stretching a sprite when apply a texture to something that is too big for it we instead just tile the image on it. 

### Example
```rust
commands.spawn((
    SpriteSheetBundle::default(),
    ImageScaleMode::Tiled {
        // The image will repeat horizontally
        tile_x: true,
        // The image will repeat vertically
        tile_y: true,
        // The texture will repeat if the drawing rect is larger than the image size
        stretch_value: 1.0,
    },
));
```

## Query transformation
### Summary 
I've made a query, and I want to pass it to another function, but I don't want to have to pass all the elements of the query to that function.
```rust
Query<(&A, &B)> -> Query<(&A)>
```

This can be done using the `QueryLens` type and `Query::transmute_lens` function.
### Example
```rust
fn reusable_function(lens: &mut QueryLens<&Transform>) {
    let query = lens.query();
    // do something with the query...
}

// We can use the function in a system that takes the exact query.
fn system_1(mut query: Query<&Transform>) {
    reusable_function(&mut query.as_query_lens());
}

// We can also use it with a query that does not match exactly
// by transmuting it.
fn system_2(mut query: Query<(&mut Transform, &Velocity), With<Enemy>>) {
    let mut lens = query.transmute_lens::<&Transform>();
    reusable_function(&mut lens);
}
```
