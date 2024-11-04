# Slabs & Plates

Slabs and Plates are popup widgets that display information to the user. They are designed to be temporary and disappear after a set duration.

Both share the same implementations but differ in their display behavior.

These widget types do not need a designated layer, as they are set to Overlay by default. Instead of a layer, enter the amount of seconds you would like the Popups to display for.

## Slabs

Display dynamically, triggered by changes in underlying text (e.g., volume detection).
```rs
Slab::new(
    factory.clone(),
    "Volume".to_string(),
    tag,
    margins,
    anchors,
    2,
)
.build();
```

## Plates

Display once at startup, then disappear after a set duration (e.g., welcome messages).
```rs
Plate::new(
    factory.clone(),
    "Greeter".to_string(),
    tag,
    margins,
    anchors,
    2,
)
.build();
```

In an attempt to retain code structure, Slabs and Plates were designed to be as similar as possible to Chunks. They share the same methods and implementations, making them interchangeable.

> Once again, for more examples, please refer to [example-chunks](https://github.com/drkrssll/example-chunks)

