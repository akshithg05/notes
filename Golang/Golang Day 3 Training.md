Encoder in go converts slices to arrays, maps to objects and arrays into arrays.

When a struct is encoded by encoder.json each exported field is encoded.
Any non exported field will not be encoded.

Every field can have another thing called tag.
Tags can be used by library devs to understand something about structure.

Different libraries use struct tags for some reason or the other. Json uses struct tags for encoding and decoding.
Not exclusively for json package, it can be used by any package 


### Concurrency

Just because its there do not use it.
It is required only if our app needs to do multiple things at the same time 
