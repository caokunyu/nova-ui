<template>
  <div class="nv-tree--wrap"></div>
</template>
<script>
  import Tree from '../../components/tree'
  export default {
    name: 'nv-tree',
    props: {
      data: {
        type: [Array, Object],
        default: []
      },
      disabled: Boolean,
      indent: {
        type: Number,
        default: 16
      },
      labelRender: Function,
      checkable: Boolean,
      radio: Boolean,
      checkName: String,
      checkStrictly: Boolean,
      expandAll: Boolean,
      highlight: Boolean,
      nodeFilter: Function,
      defaultCheckedKeys: Array,
      defaultExpandedKeys: Array,
      noDataText: String,
      noMatchDataText: String
    },
    data () {
      return {
        instance: null
      }
    },
    mounted () {
      this.instance = new Tree(this.$el, this.$props)
      this.instance
      .on('click', (node, $node) => this.$emit('click', node, $node))
      .on('expend', (status, node, $node) => this.$emit('expend', status, node, $node))
      .on('check', (status, node, $node) => this.$emit('check', status, node, $node))
    },
    methods: {
      filter (value) {
        this.instance.filter(value)
      },
      appendNode (parent, newNode) {
        this.instance.appendNode(parent, newNode)
      },
      removeNode (node) {
        this.instance.removeNode(node)
      },
      getCheckedNodes(useDisabled) {
        this.instance.getCheckedNodes(useDisabled)
      }
    },
    beforeDestroy () {
      this.instance && this.instance.destroy()
      this.$nextTick(() => this.instance = null)
    }
  }
</script>