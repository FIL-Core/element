<template>
  <transition-group tag="ul" class="el-upload__files" name="list">
    <li
      v-for="file in files"
      class="el-upload__file"
      :class="{
        'is-finished': file.status === 'finished'
      }"
      :key="file"
      @click="$emit('clickFile', file)"
    >
      <a class="el-upload__file__name" @click="$emit('preview', file)">
        <i class="el-icon-document"></i>{{file.name}}
      </a>
      <span class="el-upload__btn-delete" @click="$emit('remove', file)" v-show="file.status === 'finished'">删除</span>
      <el-progress
        v-if="file.showProgress"
        :stroke-width="2"
        :percentage="parsePercentage(file.percentage)"
        :status="file.status === 'finished' && file.showProgress ? 'success' : ''">
      </el-progress>
    </li>
  </transition-group>
</template>
<script>
  export default {
    props: {
      files: {
        type: Array,
        default() {
          return [];
        }
      }
    },
    methods: {
      parsePercentage(val) {
        return parseInt(val, 10);
      }
    }
  };
</script>
