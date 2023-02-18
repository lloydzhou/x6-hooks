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

const removeNode = useCallback((nodeId) => {
  setNodes(nodes.filter(node => node.id !== nodeId))
  // remove related edges
  setEdges(edges.filter(edge => {
    if (edge.source === nodeId || edge.source.cell === nodeId) {
      return false
    }
    if (edge.target === nodeId || edge.target.cell === nodeId) {
      return false
    }
    return true
  })
}, [nodes, edges])

const removeEdge = useCallback((edgeId) => {
  setNodes(edges.filter(edge => edge.id !== edgeId))
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
  state.setNodes([
    ...state.nodes,
    {
      id: 'id_xxx',
      ...
    }
  ])
}

const addEdge = () => {
  state.setEdges([
    ...state.edges,
    {
      source,
      target
    }
  ])
}

const removeNode = (nodeId) => {
  state.setNodes(state.nodes.filter(node => node.id !== nodeId))
  // remove related edges
  state.setEdges(state.edges.filter(edge => {
    if (edge.source === nodeId || edge.source.cell === nodeId) {
      return false
    }
    if (edge.target === nodeId || edge.target.cell === nodeId) {
      return false
    }
    return true
  })
}

const removeEdge = (edgeId) => {
  state.setNodes(state.edges.filter(edge => edge.id !== edgeId))
}

```

## examples

## react
[react demo](https://codesandbox.io/s/antv-x6-react-graph-demo-6ere13)

[mindmap demo](https://codesandbox.io/s/x6-hooks-react-mindmap-demo-2t6954?file=/src/App.js)

## vue
[vue demo](https://codesandbox.io/s/x6-hooks-vue-demo-j19slj)


