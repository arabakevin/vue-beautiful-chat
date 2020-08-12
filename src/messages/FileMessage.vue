<template>
  <div class='sc-message--file row' :style="messageColors"  :id="data.file.id">
    <div class='sc-message--file-icon'>
      <img :src="imgPreUrl(data.file.mime)" v-bind:alt="data.file.mime" class='sc-image'>
    </div>
    <div class='sc-message--file-name' :style="messageColors">
      <p>{{data.file.name || ''}}</p>
      <p>{{fileConvertSize(data.file.size) || ''}}</p>
    </div>
    <img class="download-icon" :src="icons.download.img" :alt="icons.download.name" @click="$emit('download')"/>
    <div class="sc-message--file-text" :style="messageColors">{{data.text}}<p v-if="data.meta" class='sc-message--meta' :style="messageColors">{{data.meta}}</p></div>
  </div>
</template>

<script>
import DownloadIcon from '../assets/download-icon.png'

export default {
  props: {
    data: {
      type: Object,
      required: true
    },
    messageColors: {
      type: Object,
      required: true
    },
    icons:{
      type: Object,
      default: function () {
        return {
          download:{
            img: DownloadIcon,
            name: 'download icon',
          },
        }
      }
    },
  },
  methods:{
    imgPreUrl(mime) {
      let url = ''
      if (mime == 'application/vnd.ms-excel') {
        return require(`../assets/mimes/application_vnd.ms-excel.svg`)
      }
      else if (mime == 'application/msword') {
        return require(`../assets/mimes/application_msword.svg`)
      }
      else if (mime == 'application/vnd.ms-powerpoint') {
        return require(`../assets/mimes/application_vnd.ms-powerpoint.svg`)
      }
      else if (mime == 'application/zip') {
        return require(`../assets/mimes/application_zip.svg`)
      }
      else if (mime == 'image/jpeg') {
        return require(`../assets/mimes/image_jpeg.svg`)
      }
      else if (mime == 'image/svg+xml') {
        return require(`../assets/mimes/image_svg.svg`)
      }
      else if (mime == 'text/csv') {
        return require(`../assets/mimes/text_csv.svg`)
      }
      else if (mime == 'image/png') {
        return require(`../assets/mimes/image_png.svg`)
      }
      else if (mime == 'application/pdf') {
        return require(`../assets/mimes/application_pdf.svg`)
      } else {
        return require(`../assets/mimes/default_file.svg`)
      }
    },
    fileConvertSize(aSize) {
	      aSize = Math.abs(parseInt(aSize, 10));
      	var def = [[1, 'bytes'], [1024, 'kb'], [1024*1024, 'Mb'], [1024*1024*1024, 'Gb']];
      	for(var i=0; i<def.length; i++){
      		if(aSize<def[i][0]) return (aSize/def[i-1][0]).toFixed(2)+' '+def[i-1][1];
      	}
    }
  }
}
</script>

<style scoped>
.sc-message--file {
  border-radius: 6px;
  font-weight: 300;
  font-size: 14px;
  line-height: 1.4;
  /* white-space: pre-wrap; */
  -webkit-font-smoothing: subpixel-antialiased
}

.sc-message--content.sent .sc-message--file {
  word-wrap: break-word;
  padding: 5px;
  width: 223px;
}

.sc-message--file-icon {
  text-align: center;
  margin-left: 5px;
  margin-right: auto;
  margin-bottom: 0px;
}

.sc-image {
  margin-top: 10px;
  height: 60px;
  width: 60px;
}

.sc-message--file-text {
  border-radius: 6px;
  font-weight: 300;
  font-size: 14px;
  line-height: 1.4;
  white-space: pre-wrap;
  -webkit-font-smoothing: subpixel-antialiased
}

.sc-message--file-name {
  color: white;
  padding-left: 10px;
  padding-right: 15px;
  margin-top: 10px;
  font-size: small;
  text-align: center;
  width: 107px;
}

.sc-message--file-name a {
  text-decoration: none;
  color: #ece7e7;
}

.sc-message--file-name a:hover {
  color: white;
}

.sc-message--content.sent .sc-message--file-text {
  color: white;
  background-color: #4e8cff;
  word-wrap: break-word;
}

.sc-message--content.received .sc-message--file {
  color: #263238;
  background-color: #f4f7f9;
  margin-right: 40px;
}

.sc-message--content.received .sc-message--file-name {
  color: #000;
}

.sc-message--content.received .sc-message--file a {
  color: rgba(43, 40, 40, 0.7);
}

.sc-message--content.received .sc-message--file a:hover {
  color: #0c0c0c;
}

.download-icon {
  width: 40px;
  height: 40px;
  float: right;
  margin-top: 30px;
  cursor: pointer;
}
</style>
