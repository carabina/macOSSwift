# macOSSwift: System

### Index

* [Boot Time](https://github.com/erikberglund/macOSSwift/blob/master/macOSSwift_System.md#boot-time)

## Boot Time

This function will return the kernel (system) boot date and time.

```swift
var kernelBootTime: Date? {
    
    var mib = [ CTL_KERN, KERN_BOOTTIME ]
    var bootTime = timeval()
    var bootTimeSize = MemoryLayout<timeval>.stride
    
    if 0 != Darwin.sysctl(&mib, UInt32(mib.count), &bootTime, &bootTimeSize, nil, 0) {
        Swift.print("sysctl error: Could not get HW_MEMSIZE, errno: \(errno)")
        return nil
    }
    
    return Date(timeIntervalSince1970: TimeInterval(bootTime.tv_sec))
}
````
