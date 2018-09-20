Swift
=====

## Data buffer interpretation

The following works and is valid:

    let buffer: Data = ...

    let typedArray = [Type](defaultValue, count: count)

    typedArray.withUnsafeMutableBytes {
      $0.copyBytes(from: buffer)
    }

as long as `Type` satisfies the constraints that its size times its count equals the buffer's size.
The type's memory footprint can be queried using `MemoryLayout.size(ofValue value: T) -> Int`.
It can be used in different ways:

    let x: Int = ...
    let xSize = MemoryLayout.sizeOf(value: x)

    // Or:

    let intSize = MemoryLayout<Int>.size
