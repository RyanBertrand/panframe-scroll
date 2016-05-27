# PanFrame Scroll

Related issue: http://stackoverflow.com/questions/12622800/why-does-uiscrollview-pause-my-cadisplaylink

Theory: The PanFrame NSTimer or CADisplayLink used for rendering each frame is on the incorrect NSRunLoop.  It should be added to the NSRunLoopCommonModes instead.

NSTimer Example:
```objective-c
NSTimer *renderTimer = [NSTimer timerWithTimeInterval:1/60
                                             target:self
                                           selector:@selector(renderFrame:)
                                           userInfo:nil
                                            repeats:YES];
    [[NSRunLoop mainRunLoop] addTimer:renderTimer forMode:NSRunLoopCommonModes];
```

CADisplayLink Example:
```objective-c
CADisplayLink *displayLink = [CADisplayLink displayLinkWithTarget:self selector:@selector(renderFrame)];
[displayLink addToRunLoop:[NSRunLoop mainRunLoop] forMode:NSRunLoopCommonModes];
```
