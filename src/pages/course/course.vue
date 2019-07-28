<template>
  <div class="course">
    <el-form ref="form" :inline="true" :model="form" v-if="formFlag" class="demo-form-inline" size="mini">
      <el-form-item label="课程名称">
        <el-input v-model="form.courseName"></el-input>
      </el-form-item>
      <el-form-item label="授课老师">
        <el-select v-model="form.teacherId" placeholder="请选择授课老师">
          <el-option
            v-for="teacher in teachers"
            :key="teacher.id"
            :label="teacher.name"
            :value="teacher.id"
          ></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="开始时间">
        <el-col :span="20">
          <el-date-picker
            type="date"
            placeholder="选择日期"
            v-model="form.startDate"
            style="width: 100%;"
          ></el-date-picker>
        </el-col>
      </el-form-item>
      <el-form-item label="结束时间">
        <el-col :span="20">
          <el-date-picker
            type="date"
            placeholder="选择日期"
            v-model="form.endDate"
            style="width: 100%;"
          ></el-date-picker>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="queryCourse">查询课程</el-button>
        <el-button type="primary" @click="createCourse">创建新课</el-button>
      </el-form-item>
    </el-form>
    <el-table :data="coures" style="width: 100%" v-if="courseViewFlag"> 
      <el-table-column label="课程ID" width="180">
        <template slot-scope="scope">
          <span style="margin-left: 10px">{{ scope.row.courseId }}</span>
        </template>
      </el-table-column>
      <el-table-column label="课程名称" width="180">
        <template slot-scope="scope">
          <span style="margin-left: 10px">{{ scope.row.courseName }}</span>
        </template>
      </el-table-column>
      <el-table-column label="授课老师" width="180">
        <template slot-scope="scope">
          <span style="margin-left: 10px">{{ scope.row.teacherName }}</span>
        </template>
      </el-table-column>
      <el-table-column label="发布时间" width="180">
        <template slot-scope="scope">
          <i class="el-icon-time"></i>
          <span style="margin-left: 10px">{{ scope.row.pubtime }}</span>
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button size="mini" @click="managerCourse(scope.row)">管理</el-button>
          <!-- <el-button size="mini" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button> -->
        </template>
      </el-table-column>
    </el-table>

    <el-form ref="form"  :model="courseDetail" v-if="courseDetailFlag" class="demo-form-inline" size="mini">
      <el-form-item label="课程名称">
        <el-input v-model="courseDetail.courseName"></el-input>
      </el-form-item>
      <el-form-item label="授课老师">
        <el-select v-model="courseDetail.teacherId" placeholder="请选择授课老师">
          <el-option
            v-for="teacher in teachers"
            :key="teacher.id"
            :label="teacher.name"
            :value="teacher.id"
          ></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="发布时间">
        <el-col :span="20">
          <el-date-picker
            type="date"
            placeholder="选择日期"
            v-model="courseDetail.pubtime"
            style="width: 100%;"
          ></el-date-picker>
        </el-col>
      </el-form-item>
      <el-upload
        class="upload-demo"
        action="https://jsonplaceholder.typicode.com/posts/"
        :on-preview="handlePreview"
        :on-remove="handleRemove"
        :file-list="fileList"
        list-type="picture">
        <el-button size="small" type="primary">点击上传</el-button>
      </el-upload>
      <el-form-item>
        <el-button type="primary" @click="saveCourse">保存</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      form: {
        courseName: '',
        teacherId: '',
        startDate: '',
        endDate: ''
      },
      courseDetail: {
        courseId: '',
        courseName: '',
        teacherId: '',
        teacherName: '',
        pubtime: '',
        models: []
      },
      teachers: [{ id: 1, name: '曹老师' }, { id: 2, name: '杨老师' }],
      models: [{ id: 1, name: '限时免费' }, { id: 2, name: '杨老师' }],
      formFlag: true,
      courseViewFlag: false,
      courseDetailFlag: false,
      coures: [{ courseId: 1, courseName: '你是哪种类型的父母', teacherName: '曹老师', teacherId: 1, pubtime: '2019-07-21' },
      { courseId: 2, courseName: '怎样”命令” 孩子才会听', teacherName: '曹老师', teacherId: 1, pubtime: '2019-07-21' }]
    };
  },
  methods: { 
    init() {
      this.getAllTeachers();
      this.getAllModels();
    },
    getAllTeachers() {
      
    },
    getAllModels() {
      this.models = [];
    },
    queryCourse() {
      // TODO 按条件查询课程
      this.courseViewFlag = true;
    },
    createCourse() {
      this.courseViewFlag = false;
    },
    managerCourse(course) {
      this.formFlag = false;
      this.courseViewFlag = false;
      this.courseDetail.courseId = course.courseId;
      this.courseDetail.courseName = course.courseName;
      this.courseDetail.teacherId = course.teacherId;
      this.courseDetail.teacherName = course.teacherName;
      this.courseDetail.pubtime = course.pubtime;
      this.courseDetailFlag = true;
    },
    saveCourse() {
      
    }
  }
};
</script>

