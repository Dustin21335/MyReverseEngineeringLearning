I noticed that some tools were disabled and marked **(Pro Only)**. I searched the strings and found `'intersect' is a Pro only feature.`

That led me to the function at `0x1407378f0`, which looks like the function used to start the intersect tool. The function first calls `0x1405fcf50`, and if it returns `false`, it calls `rb_raise` with the **"intersect is a Pro only feature"** error.

```text
14073792e    if (sub_1405fcf50() == 0)
140737941        rb_raise(*rb_eArgError, "'intersect' is a Pro only feature.")
```

After following the call to `0x1405fcf50`, I found that it checks a pointer at `0x1411ce500`. If the pointer exists, it jumps through its vtable at `+0x8`; otherwise, it falls back to returning `0`.

```text
1405fcf50    int64_t sub_1405fcf50()

1405fcf50        int64_t* rcx = data_1411ce500

1405fcf5a        if (rcx != 0)
1405fcf5f            jump(*(rcx + 8))

1405fcf63        int64_t result
1405fcf63        result.b = 0
1405fcf65        return result
```

This appears to be the `IsPro` check.

I patched the check so that it always returns `true`. Woohoo, now we have the Pro only tools. 

```text
1405fcf50    int64_t sub_1405fcf50()

1405fcf57        return 1
```

SketchUp Make 2017 installer is available from the [Internet Archive](https://archive.org/details/sketchupmake2017).
