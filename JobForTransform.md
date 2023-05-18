```C#
struct PositionUpdateJob : IJobParallelForTransform
{
    [ReadOnly]
    public NativeArray<float3> positions;

    // 实现IJobParallelForTransform的结构体中Execute方法第二个参数可以获取到Transform
    public void Execute(int i, TransformAccess transform)
    {
        transform.position =position
    }
}
```

```C#   
var positions = new NativeArray<Vector3>(100, Allocator.Persistent)
var transforms = new Transform[100];
var transformsAccessArray = new TransformAccessArray(transforms);

var job = new PositionUpdateJob()
{
    positions = positions,
}.Schedule(transformsAccessArray);
```

