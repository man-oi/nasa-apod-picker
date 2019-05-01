<template>
  <div class="home">
    <el-row :gutter="20">
      <el-col :span="6">
        <el-date-picker
          v-model="selectedDate"
          :picker-options="dateOptions"
          :clearable="false"
          type="date"
        />
      </el-col>
      <el-col :span="18">
        <apod-image v-if="selectedDate" :date="selectedDate" />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import moment from 'moment';

// @ is an alias to /src
import ApodImage from '@/components/Apod-Image.vue';

export default {
  name: 'home',

  components: {
    ApodImage,
  },

  data() {
    return {
      selectedDate: moment().subtract(1, 'days').toDate(),
      dateOptions: {
        disabledDate(time) {
          return (
            time.getTime() >= moment().subtract(1, 'days').valueOf()
            || time.getTime() < new Date('1995-06-15').getTime()
          );
        },
      },
    };
  },
};
</script>
