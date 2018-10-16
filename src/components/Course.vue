<template>
  <div class="course">
    <el-container style="display: inline-flex; flex: 1; margin: 20px; border: 1px solid #eee">
      <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
        <div v-for="o in this.courses" :key="o.id" class="text item">
          <el-card class="box-card">
            <div>{{o.name}}</div>
            <div>
              <span>包含内容 </span>
              <span style="color: blue;font-size: 18px;">{{o.list.length}}</span>
              <span> 组</span>
            </div>
            <div>
              <el-button v-on:click="selectCourse(o, 0)" type="text">看音识字</el-button>
              <el-button v-on:click="selectCourse(o, 1)" type="text">看音识字</el-button>
            </div>
          </el-card>
        </div>
      </el-aside>

      <el-container>
        <el-header>
          <span>当前得分：</span>
          <span style="color: red; font-size: 20px">{{score}}</span>
        </el-header>

        <el-main>
          <div style="color: blue; font-size: 28px; margin-top: 20px">{{question}}</div>
          <div>
            <input
              v-model="answer"
              v-if="this.question"
              @keyup.right="next()"
              style="height: 50px; margin-top: 20px; font-size: 28px; color: #333; text-align: center"
            />
          </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
  let data = require('../words/words.json')
  export default {
    name: 'HelloWorld',
    data () {
      const item = {
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }
      return {
        courses: data.courses,
        tableData: Array(20).fill(item),
        type: 0,
        course: { list: [] },
        courseListIndex: 0,
        answer: '',
        results: []
      }
    },
    computed: {
      disorderCourseList: function () {
        function randomsort(a, b) {
          return Math.random() > 0.5 ? -1 : 1
        }

        this.course.list.sort(randomsort)
        return this.course.list
      },
      question: function() {
        const type = this.type === 0 ? 'spell' : 'word'
        const obj = this.disorderCourseList[this.courseListIndex]
        return obj ? obj[type] : ''
      },
      score: function() {
        let count = 0
        for (let o of this.results) {
          if (o.answer === o.correctAnswer) {
            count++
          }
        }

        return this.disorderCourseList && this.disorderCourseList.length
          ? Math.ceil(count / this.disorderCourseList.length * 100)
          : 0
      }
    },
    methods: {
      selectCourse: function(o, t) {
        this.course = o
        this.type = t
        this.courseListIndex = 0
        this.results = []
      },
      next: function(ev) {
        const qType = this.type === 0 ? 'spell' : 'word'
        const aType = this.type === 0 ? 'word' : 'spell'
        const question = this.disorderCourseList[this.courseListIndex]
        let obj = {
          question: question[qType],
          answer: this.answer,
          correctAnswer: question[aType]
        }
        this.results.push(obj)
        this.answer = ""

        if (this.courseListIndex < this.disorderCourseList.length - 1) {
          this.courseListIndex++
        }
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .course {
    flex: 1;
    display: flex;
  }
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
  }

  .el-aside {
    color: #333;
  }
</style>
