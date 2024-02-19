# O1JS is not quite compatible with NodeNext module resolution

`src/index.ts` contains a simple program that gets _exported_:

```typescript
import { Bool, Field, ZkProgram } from "o1js";

export const HelloProgram = ZkProgram({
    name: "hello-program",
    publicInput: Field,
    publicOutput: Bool,
    methods: {
        addition: {
            privateInputs: [Field, Field],
            method(sum, a, b) {
                return a.add(b).equals(sum);
            },
        },
    },
});
```

Nothing criminal here, but it can not be compiled by TS compiler while using `NodeNext` module resolution algorithm.

If you go to `tsconfig.json` and change `"moduleResolution": "NodeNext",` to `"moduleResolution": "Node",` it works okay though.