# x6-hooks

以数据驱动x6画布

## react

```
import { useGraphState } from 'x6-hooks/react'

const { nodes, setNodes, edges, setEdges, graph, setGraph } = useGraphState()

useEffect(() => {
  const graph = new X6.Graph({ ...  })
  setGraph(graph)
}, [])

const addNode = useCallback(() => {
  // add node to nodes array
  setNodes([
    ...nodes,
    {
      id: 'id_xxx',
      ...
    }
  ])
}, [nodes])

const addEdge = useCallback(() => {
  setEdges([
    ...edges,
    {
      source,
      target
    }
  ])
}, [edges])

```

## vue

```
import { useGraphState } from 'x6-hooks/vue'

// 这里不能直接解包，直接解包之后可能导致拿到的nodes不变化
const state = useGraphState()

onMounted(() => {
  const { setNodes, setEdges, setGraph } = state
  const graph = new X6.Graph({ ...  })
  setGraph(graph)

  // init data
  setNodes([...])
  setEdges([...])
})

const addNode = () => {
  // add node to nodes array
  setNodes([
    ...nodes,
    {
      id: 'id_xxx',
      ...
    }
  ])
}

const addEdge = () => {
  setEdges([
    ...edges,
    {
      source,
      target
    }
  ])
}

```

## examples

[react demo](https://codesandbox.io/s/antv-x6-react-graph-demo-6ere13)

[vue demo](https://codesandbox.io/s/x6-hooks-vue-demo-j19slj)


