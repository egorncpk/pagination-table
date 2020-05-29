<template>
  <div class="content">
    <div class="row header">
      <div class="column sort" style="max-width: 120px;" @click="sortArray('date')">
        Дата
        <svg class="icon" :style="`display: ${sort.date === 0 ? 'none' : 'block'}; ${sort.date === -1 ? 'transform: rotate(270deg);' : ''}`">
          <use xlink:href="#icon-arrow"></use>
        </svg>
      </div>
      <div class="column sort" @click="sortArray('name')">Название курса
        <svg class="icon" :style="`display: ${sort.name === 0 ? 'none' : 'block'}; ${sort.date === -1 ? 'transform: rotate(270deg);' : ''}`">
          <use xlink:href="#icon-arrow"></use>
        </svg>
      </div>
    </div>
    <div class="list__rows" v-for="item in courseArray" v-bind:key="item.name">
      <div class="row">
        <div class="column" style="max-width: 120px;">{{item.date}}</div>
        <div class="column">{{item.name}}</div>
      </div>
    </div>
    <div class="row footer">
      <div class="column">Страница:</div>
      <div class="column" v-for="el in pagination.maxPage" v-bind:key="el" style="max-width: 25px; justify-content: center;" @click="nextPage(el)">
        <div class="page" :class="pagination.page === el ? 'active' : ''">{{el}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Table',
  data () {
    return {
      courseArray: [],
      pagination: {
        page: 1,
        maxPage: 1,
        count: 3
      },
      sort: {
        name: 0,
        date: 0
      }
    }
  },
  props: {
    rowArray: Array
  },
  methods: {
    sortArray (field) {
      const sortArr = [...this.courseArray]
      this.courseArray = []

      Object.keys(this.sort).forEach(item => { if (item !== field) this.sort[item] = 0 })

      this.sort[field] = this.sort[field] === -1 ? 0 : this.sort[field] === 0 ? 1 : -1

      if (this.sort[field] === 0) this.courseArray = [...this.rowArray.slice(this.pagination.page * this.pagination.count - this.pagination.count, this.pagination.page * this.pagination.count)]
      else {
        Array.prototype.sort.call(sortArr, (a, b) => {
          a = field === 'date' ? new Date(a[field].replace(/(\d{2}).(\d{2}).(\d{4})/, '$2/$1/$3')) : a[field]
          b = field === 'date' ? new Date(b[field].replace(/(\d{2}).(\d{2}).(\d{4})/, '$2/$1/$3')) : b[field]
          return a > b ? this.sort[field] : a < b ? this.sort[field] * -1 : 0
        })

        this.courseArray = [...sortArr]
      }
    },
    nextPage (page) {
      Object.keys(this.sort).forEach(item => { this.sort[item] = 0 })
      this.pagination.page = page
      this.courseArray = [...this.rowArray.slice(this.pagination.page * this.pagination.count - this.pagination.count, this.pagination.page * this.pagination.count)]
    }
  },
  mounted () {
    this.pagination.maxPage = Math.ceil(this.rowArray.length / this.pagination.count)
    this.courseArray = [...this.rowArray.slice(0, 3)]
  }
}
</script>

<style lang="less" scoped>

  .list__rows {
    position: relative;
    display: flex;
    flex-direction: column;
    border: 1px solid transparent;
    border-top-color: #cad5db;
    border-bottom-color: #cad5db;
    padding: 8px 4px;
    overflow: hidden;

    &:hover {
      background-color: #f4f7fc;
    }
  }

  .header {
    background-color: #512da8;
    color: #a7a2af;

    .sort {
      cursor: pointer;
      &:hover {
        color: #fff;
      }

      .icon {
        margin-left: 20px;
        transform: rotate(90deg);
        height: 12px;
        width: 12px;
      }
    }
  }

  .footer {
    .page {
      display: flex;
      justify-content: center;
      width: 25px;
      height: 25px;
      border-radius: 50%;
      align-items: center;
      cursor: pointer;

      &:hover {
        box-sizing: border-box;
        border-color: #512da8;
        border-style: solid;
        transform: scale(1.2);
      }
    }

    .active {
      color: #fff;
      background-color: #512da8;
    }
  }

  .row {
    display: flex;
    flex-direction: row;
    flex: 1 1 100%;

    .column {
      position: relative;
      display: flex;
      flex: 1 1 100%;
      padding: 0 8px;
      overflow: hidden;
      align-items: center;
      text-align: left;
      height: 40px;
    }

  }
</style>
