# x6-hooks

以数据驱动x6画布

<a href="https://www.npmjs.com/package/x6-hooks"><img alt="NPM Package" src="https://img.shields.io/npm/v/x6-hooks.svg?style=flat-square"></a>
![npm bundle size](https://img.shields.io/bundlephobia/minzip/x6-hooks?style=flat-square)
![npm](https://img.shields.io/npm/dm/x6-hooks?style=flat-square)
<a href="/LICENSE"><img src="https://img.shields.io/github/license/lloydzhou/x6-hooks?style=flat-square" alt="MIT License"></a>

## install
```
npm install x6-hooks
yarn add x6-hooks
```

## online demos
### react
[react demo](https://codesandbox.io/s/antv-x6-react-graph-demo-6ere13)

[mindmap demo](https://codesandbox.io/s/x6-hooks-react-mindmap-demo-2t6954?file=/src/App.js)

### vue
[vue demo](https://codesandbox.io/s/x6-hooks-vue-demo-j19slj)


## examples
### react
```
import { useGraphState } from 'x6-hooks/react'

const { nodes, setNodes, edges, setEdges, graph, setGraph } = useGraphState()

// setNodes and setEdges return Promise

useEffect(() => {
  const graph = new X6.Graph({ ...  })
  setGraph(graph)

  // init data
  setNodes([...])
  setEdges([...])
}, [])

const addNode = useCallback((node: Node.Metadata) => {
  // add node to nodes array
  setNodes([...nodes, node])
}, [nodes])

const addEdge = useCallback((edge: Edge.Metadata) => {
  setEdges([...edges, edge])
}, [edges])

const updateNode = useCallback((nodeId: string, node: Node.Metadata) => {
  const index = nodes.findIndex(node => node.id === nodeId)
  if (index > -1) {
    nodes[index] = node
    setNodes([...nodes])
  }
}, [nodes])

const updateEdge = useCallback((edgeId: string, edge: Edge.Metadata) => {
  const index = edges.findIndex(edge => edge.id === edgeId)
  if (index > -1) {
    edges[index] = edge
    setEdges([...edges])
  }
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
  setEdges(edges.filter(edge => edge.id !== edgeId))
}, [edges])

```

### vue

```
import { useGraphState } from 'x6-hooks/vue'

const { nodes, edges, graph, setNodes, setEdges, setGraph } = useGraphState()

// setNodes and setEdges return Promise

onMounted(() => {
  const graph = new X6.Graph({ ...  })
  setGraph(graph)

  // init data
  setNodes([...])
  setEdges([...])
})

const addNode = (node: Node.Metadata) => {
  // add node to nodes array
  setNodes([
    ...nodes.value,  // nodes is ref
    node,
  ])
}

const addEdge = (edge: Edge.Metadata) => {
  setEdges([
    ...edges.value, // edges is ref
    edge,
  ])
}

const updateNode = (nodeId: string, node: Node.Metadata) => {
  const index = nodes.value.findIndex(node => node.id === nodeId)
  if (index > -1) {
    nodes.value[index] = node
    setNodes([...nodes.value])
  }
}

const updateEdge = (edgeId: string, edge: Edge.Metadata) => {
  const index = edges.value.findIndex(edge => edge.id === edgeId)
  if (index > -1) {
    edges.value[index] = edge
    setEdges([...edges.value])
  }
}

const removeNode = (nodeId) => {
  setNodes(nodes.value.filter(node => node.id !== nodeId))
  // remove related edges
  setEdges(edges.value.filter(edge => {
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
  setEdges(edges.value.filter(edge => edge.id !== edgeId))
}

```

## 集成
配合[x6-graph](https://github.com/lloydzhou/x6-graph)使用

1. 使用x6-hooks管理数据
2. 使用x6-graph封装图实例
3. x6-graph子组件的模式对业务逻辑做拆分组合（也可以用这个模式抽象一些常用的组件，例如将官方的plugin抽象成UI组件挂载到Graph内部）


