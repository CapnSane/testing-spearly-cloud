<script lang="ts">
import * as axios from "axios";
// import { upload } from './file-upload.service';

const BASE_URL = "http://localhost:3001";

function upload(formData: any) {
  const url = `${BASE_URL}/photos/upload`;

  return (
    axios
      .post(url, formData)
      // get data
      .then((x: any) => x.data)
      // add url field
      .then((x: any) =>
        x.map((file: any) => Object.assign({}, file, { url: `${BASE_URL}/images/${file.id}` })),
      )
  );
}

export { upload };

const STATUS_INITIAL = 0,
  STATUS_SAVING = 1,
  STATUS_SUCCESS = 2,
  STATUS_FAILED = 3;

export default {
  name: "app",
  data() {
    return {
      uploadedFiles: [],
      uploadError: null,
      currentStatus: null,
      uploadFieldName: "photos",
    };
  },
  computed: {
    isInitial() {
      return this.currentStatus === STATUS_INITIAL;
    },
    isSaving() {
      return this.currentStatus === STATUS_SAVING;
    },
    isSuccess() {
      return this.currentStatus === STATUS_SUCCESS;
    },
    isFailed() {
      return this.currentStatus === STATUS_FAILED;
    },
  },
  methods: {
    reset() {
      // reset form to initial state
      this.currentStatus = STATUS_INITIAL;
      this.uploadedFiles = [];
      this.uploadError = null;
    },
    save(formData) {
      // upload data to the server
      this.currentStatus = STATUS_SAVING;

      upload(formData)
        .then((x) => {
          this.uploadedFiles = [].concat(x);
          this.currentStatus = STATUS_SUCCESS;
        })
        .catch((err) => {
          this.uploadError = err.response;
          this.currentStatus = STATUS_FAILED;
        });
    },
    filesChange(fieldName, fileList) {
      // handle file changes
      const formData = new FormData();

      if (!fileList.length) return;

      Array.from(Array(fileList.length).keys()).map((x) => {
        formData.append(fieldName, fileList[x], fileList[x].name);
      });

      this.save(formData);
    },
  },
  mounted() {
    this.reset();
  },
};
</script>

<template>
  <div id="app">
    <div class="container">
      <form enctype="multipart/form-data" novalidate v-if="isInitial || isSaving">
        <h1>Upload files</h1>
        <div class="dropbox">
          <input
            type="file"
            multiple
            :name="uploadFieldName"
            :disabled="isSaving"
            @change="
              filesChange($event.target.name, $event.target.files);
              fileCount = $event.target.files.length;
            "
            accept="image/*"
            class="input-file"
          />
          <p v-if="isInitial">
            Drag your file(s) here to begin<br />
            or click to browse
          </p>
          <p v-if="isSaving">Uploading {{ fileCount }} files...</p>
        </div>
      </form>
    </div>
  </div>
</template>

<style lang="scss">
.dropbox {
  outline: 2px dashed grey;
  outline-offset: -10px;
  background: lightcyan;
  color: dimgray;
  padding: 10px 10px;
  min-height: 200px;
  position: relative;
  margin: 0 200px;
  cursor: pointer;
}

.input-file {
  opacity: 0;
  width: fit-content;
  height: 200px;
  position: absolute;
  cursor: pointer;
}

.dropbox:hover {
  background: lightblue;
}

.dropbox p {
  font-size: 1.2em;
  text-align: center;
  padding: 50px 0;
}
</style>
