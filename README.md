# x6-hooks

以数据驱动x6画布

## react

```
import { useGraphState } from 'x6-hooks/react'
```

## vue

```
import { useGraphState } from 'x6-hooks/vue'

```

## examples

```
// import { useGraphState } from '...'

const { nodes, setNodes, edges, setEdges, graph, setGraph } = useGraphState()

const graph = new X6.Graph({ ...  })

setGraph(graph)

setNodes([{
  id: 'node1',
  ...
})

setEdges([{ ... }])

```

