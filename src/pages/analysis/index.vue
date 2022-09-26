<template>
  <a-row>
    <a-breadcrumb >
      <a-breadcrumb-item>
        <home-outlined />
      </a-breadcrumb-item>
      <a-breadcrumb-item>Análisis</a-breadcrumb-item>
    </a-breadcrumb>
    <div class="upload-container">
      <a-card class="upload-card" :head-style="{textAlign: 'center'}" title="Adjunte su oficio aquí">
        <a-upload-dragger
            name="file"
            class="upload"
            :multiple="true"
            :before-upload="beforeUpload"
            action="https://www.mocky.io/v2/5cc8019d300000980a055e76"
            @change="handleChange"
        >
          <div class="ant-upload-drag-container">
            <p class="upload-text">Drop files here or click to upload</p>
            <p class="upload-hint">
              (This is just a demo dropzone. Selected files are not actually uploaded.)
            </p>
          </div>
        </a-upload-dragger>
        <template #actions>
          <a-row justify="center">
            <a-col :span="4">
              <a-button style="color:#82868B">Cancelar</a-button>
            </a-col>
            <a-col>
              <a-button type="primary" >Realizar Análisis</a-button>
            </a-col>
          </a-row>
        </template>
      </a-card>
    </div>
  </a-row>

</template>

<script>
import { HomeOutlined } from '@ant-design/icons-vue';

export default {
  components: {
    HomeOutlined,
  },
  name: "index",
  methods: {
    handleChange({file}) {
      const {status} = file;
      this.status = status;

      if (status === 'done') {
        this.uploaded = true;
        return this.$message.success(`${file.name} subido correctamente.`);
      }

      if (status === 'error') {
        return this.$message.error(`${file.name} ha fallado al subir.`);
      }
    },
    beforeUpload(file) {
      const isLt1GB = file.size / 1024 < 1048;
      console.log(file.size);
      if (!isLt1GB) {
        this.$message.error('Sólo puedes subir archivos menores a 1GB!');
      }
      return isLt1GB;
    },
  }
}
</script>

<style scoped>
.upload-container {
  background-color: #BABFC7;
  width: 100%;
  margin-top: 30px;
  min-height: 450px;
}
.upload-card ::v-deep(.ant-upload) {
  min-height: 250px;
}
.upload-card ::v-deep(.ant-card-body) {
  padding: 0 50px;
}
.upload-hint {
  color: #BF0909 !important;
  font-family: 'Montserrat', sans-serif;
  font-weight: 300;
  font-size: 14px;
}
.upload-text {
  color: #BF0909 !important;
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
  font-size: 19px;
  padding-bottom: 15px;
}
.upload-card ::v-deep(.ant-upload-drag-container)  {
  display: table-cell;
  vertical-align: middle;
}
.upload-card {
  margin: 30px 120px;
}
.upload-card ::v-deep(.ant-card-head-title) {
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
  font-size: 21px;
  margin-top: 30px;
}
</style>