<template>
  <div class="hello">
    <el-header>
    </el-header>
    <el-main>
      <el-table
        :data="tableData"
        style="width: 100%">
        <el-table-column
          label="文件名">
          <template slot-scope="scope">
            <i class="el-icon-time"></i>
            <span style="margin-left: 10px">{{ scope.row.name }}</span>
          </template>
        </el-table-column>
        <el-table-column label="操作" width="180">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.$index, scope.row)">分享
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </el-main>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tableData: []
    }
  },
  created () {
    this.loadData()
  },
  methods: {
    loadData () {
      console.log('1')
      const path = require('path')
      console.log(path)
      require.context('../../static', false, /.pdf$/).keys().forEach(item => {
        console.log(item)
        this.tableData.push({
          name: item
        })
      })
    },
    handleEdit (index, row) {
      console.log(index, row)
      let download = '/static/file/' + this.tableData[index].name.substr(2)
      if (location.href.toString().indexOf('git') > -1) {
        download = '/git-pan' + download
      }
      window.open(download, '_blank')
    },
    handleDelete (index, row) {
      console.log(index, row)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
