<template>
  <div class='sc-message--file row' :style="messageColors"  :id="data.file.id">
    <div class='sc-message--file-icon'>
      <img :src="imgPreUrl(data.file.mime)" v-bind:alt="data.file.mime" class='sc-image'>
    </div>
    <div class='sc-message--file-name' :style="messageColors">
      <p v-if="data.file.name.length > 16">{{ data.file.name.substring(0,16) + '...' || ''}}</p>
      <p v-if="data.file.name.length <= 16">{{ data.file.name || ''}}</p>
    </div>
    <div class='sc-message--file-size' :style="messageColors">
      <p>{{fileConvertSize(data.file.size) || ''}}</p>
    </div>
    <div class='sc-message--file-icons' :style="messageColors">
      <svg class="download-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50" width="30px" height="30px" @click="$emit('download')">
        <path fill="none" stroke="#000000" stroke-miterlimit="10" stroke-width="2" d="M31 28L25 34 19 28"/>
        <path fill="none" stroke="#000000" stroke-miterlimit="10" stroke-width="2" d="M31 28L25 34 19 28"/>
        <path fill="none" stroke="#000000" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="2" d="M25 20L25 34"/>
        <path fill="none" stroke="#000000" stroke-linecap="round" stroke-miterlimit="10" stroke-width="2" d="M43,24.3c0-0.1,0-0.2,0-0.3c0-5.5-4.5-10-10-10c-1.2,0-2.3,0.2-3.4,0.6C27.7,11.3,24.1,9,20,9C13.9,9,9,13.9,9,20c0,0.1,0,0.1,0,0.2c-4.6,0.9-8,5-8,9.8c0,5.5,4.5,10,10,10c5.2,0,26.3,0,30,0c4.4,0,8-3.6,8-8C49,28.3,46.4,25.1,43,24.3z"/>
      </svg>
    </div>
    <div class="sc-message--file-text" :style="messageColors">{{data.text}}<p v-if="data.meta" class='sc-message--meta' :style="messageColors">{{data.meta}}</p></div>
  </div>
</template>

<script>

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

<style lang="scss">
.sc-message--file {
  border-radius: 6px;
  font-weight: 300;
  font-size: 14px;
  line-height: 1.4;
  -webkit-font-smoothing: subpixel-antialiased
}

.sc-message--content.sent .sc-message--file {
  word-wrap: break-word;
  padding: 5px;
  width: 223px;
}

.sc-message--file-icon {
  z-index: 1;
}

.sc-image {
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
  margin-top: 7px;
  font-size: small;
  text-align: left;
  width: 148px;
}

.sc-message--file-size {
    margin-top: -35px;
    font-size: small;
    text-align: left;
    margin-left: 64px;
    width: 60px;
    height: 10px;
    z-index: 1;
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

.sc-message--file-icons {
  width: 190px;
  margin-top: -30px;
}

.sc-message--content.sent {
  fill: #000000;
  .download-icon {
    fill: #ffffff;
    path {
      stroke: #ffffff;
    }
  }
  .sc-image {
    filter: invert(100%) sepia(12%) saturate(24%) hue-rotate(26deg) brightness(104%) contrast(107%)
  }
}

.download-icon, .sc-message--file-icon {
  float: right;
  cursor: pointer;
}
</style>
