<template>
  <div id="app">
    <componentTable :rowArray="coursesData"/>
  </div>
</template>

<script>
import componentTable from './components/table.vue'

export default {
  name: 'App',
  components: {
    componentTable
  },
  data () {
    return {
      coursesData: [
        {
          name: 'Противодействие коррупции',
          date: '28.02.2018'
        },
        {
          name: 'Обучение JS. Часть 1',
          date: '27.02.2018'
        },
        {
          name: 'Рекурсивные запросы MS SQL Server 2012',
          date: '02.02.2019'
        },
        {
          name: 'Управление IT-инфраструктурой (ITSM)',
          date: '11.05.1992'
        },
        {
          name: '2.0 Эффективный менеджмент в организации',
          date: '11.05.1992'
        },
        {
          name: 'Подготовка к сертификации SOA (PEOPLECERT Intermediate SOA)',
          date: '28.03.2019'
        },
        {
          name: 'Эффективный тайм - менеджмент для специалиста с использованием Microsoft Outlook 2019/2016',
          date: '27.05.2019'
        },
        {
          name: '0.9 Эффективный тайм - менеджмент для специалиста с использованием Microsoft Outlook 2019/2016',
          date: '02.02.2019'
        },
        {
          name: '',
          date: '11.05.1992'
        },
        {
          name: 'Кибербезопасность 4.0',
          date: '11.05.1992'
        }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  max-width: 1200px;
}
</style>
