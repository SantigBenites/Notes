Normal OSes are usable in real-time

Linux for example isn't real-time because:
- Applications run in user space
- Hardware interaction is done in the kernel
- Kernel isn't preempted by threads

Because the kernel doesn't have the needed real-time properties

So there is a need for a real-time kernel which will allow us to
- Abstract away timing information
- Maintainability/Extensibility
- Molecularity
- Team Development

Real-time Co-kernel Linux