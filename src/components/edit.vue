<template>
  <div class="edit-container">
    <div class="edit-div">
      <!-- 撤销/取消撤销 -->
      <div class="icon-undo2 icon-class" @click="textUndo"></div>
      <div class="icon-redo2 icon-class" @click="textRedo"></div>
      <!-- 加粗 -->
      <div class="icon-bold icon-class" @click="textStrong"></div>
      <!-- 倾斜 -->
      <div class="icon-italic icon-class" @click="textItalic"></div>
      <!-- 下划线 -->
      <div class="icon-underline icon-class" @click="textUnderline"></div>
      <!-- 字体 -->
      <select class="select-class" v-model="selectFontFamily" name="font-size">
        <option value="YaHei">雅黑</option>
        <option value="SimSun">宋体</option>
        <option value="YouYuan">幼圆</option>
        <option value="KaiTi">楷体</option>
      </select>
      <!-- 字体大小 -->
      <select class="select-class" v-model="selectFontSize" name="font-size">
        <option value="1">1号</option>
        <option value="2">2号</option>
        <option value="3">3号</option>
        <option value="4">4号</option>
        <option value="5">5号</option>
        <option value="6">6号</option>
        <option value="7">7号</option>
      </select>
      <!-- 标题 -->
      <select class="select-class" v-model="selectHead" name="font-size">
        <option value="h1">一号标题</option>
        <option value="h2">二号标题</option>
        <option value="h3">三号标题</option>
        <option value="h4">四号标题</option>
        <option value="h5">五号标题</option>
        <option value="h6">六号标题</option>
        <option value="h7">七号标题</option>
        <option value="p">普通文本</option>
      </select>
      <!-- 字体颜色 -->
      <div>
        <div :style="iconFontColor" class="icon-delicious icon-class" @click="showChangeColorMenu"></div>
        <ul class="change-color-menu" v-show="isChangeColorMenu">
          <!-- 展示颜色块 -->
          <!-- 注意这里必须是button 否则不能触发 -->
          <button
            v-for="item in fontIconMenuColorBlock"
            :class="item"
            :key="item"
            @click="textChangeClor(item)"
          ></button>
        </ul>
      </div>

      <!-- 背景颜色 -->
      <div>
        <div class="icon-pen icon-class" @click="showChangeBackgroundColorMenu"></div>
        <ul class="change-color-menu" v-show="isChangeBackgroundColorMenu">
          <button
            v-for="item in fontIconMenuBackgroundColorBlock"
            :class="item"
            :key="item"
            @click="textChangeBackgroundClor(item)"
          ></button>
        </ul>
      </div>

      <!-- 清除格式 -->
      <div class="icon-scissors icon-class" @click="textRemoveAll"></div>
      <!-- 有序列表 -->
      <div class="icon-list-numbered icon-class" @click=" textOrderList"></div>
      <!-- 无序列表 -->
      <div class="icon-list2 icon-class" @click="textUnorderList"></div>
      <!-- 左对齐 -->
      <div class="icon-paragraph-left icon-class" @click="textJustifyleft"></div>
      <!-- 居中 -->
      <div class="icon-paragraph-center icon-class" @click="textJustifycenter"></div>
      <!-- 缩进 -->
      <div class="icon-indent-increase icon-class" @click="textIndent"></div>
      <!-- 取消缩进 -->
      <div class="icon-indent-decrease icon-class" @click="textOutdent"></div>
      <!-- 图片 -->
      <div class="icon-image icon-class"></div>
      <!-- 表情 -->
      <div>
        <div class="icon-happy icon-class" @click="showEmotionMenu"></div>
        <div class="emotion-menu-class" v-show="isShowEmotionMunu">
          <img
            v-for="item in emotionPngSrc"
            :key="item"
            :src="item"
            class="emotion-menu-item-class"
            @click="textEmotion(item)"
            alt="404"
          />
        </div>
      </div>
      <!-- 全屏 -->
      <div id="fullScreen" class="icon-class" :class="fullScreen" @click="textFullScreen"></div>
      <!-- 保存 -->
      <div class="icon-floppy-disk icon-class"></div>
    </div>
    <div class="edit-main defaut-font" contenteditable="true"></div>
  </div>
</template>

<script>
export default {
  name: "edit",
  data() {
    return {
      publicPath: process.env.BASE_URL,
      selectFontFamily: "YaHei",
      selectFontSize: "3",
      selectHead: "p",
      isChangeColorMenu: false,
      isChangeBackgroundColorMenu: false,
      isShowEmotionMunu: false,
      //文字颜色菜单里的块颜色
      fontIconMenuColorBlock: [
        "change-color-red",
        "change-color-yellow",
        "change-color-blue",
        "change-color-green",
        "change-color-black"
      ],
      //fontcolor图标的颜色(弃用)
      iconFontColor: "",
      //背景颜色菜单里的块颜色
      fontIconMenuBackgroundColorBlock: [
        "change-color-skyblue",
        "change-color-yellow",
        "change-color-white"
      ],
      //表情连接
      emotionPngSrc: [
        "/emotion/joy.png",
        "/emotion/blush.png",
        "/emotion/smiley.png",
        "/emotion/wink.png",
        "/emotion/scream.png",
        "/emotion/sob.png",
        "/emotion/fearful.png",
        "/emotion/heart_eyes.png"
      ],
      fullScreen: "icon-enlarge"
    };
  },
  watch: {
    immediate: true,
    //修改字体
    selectFontFamily(newVal) {
      switch (newVal) {
        case "YaHei": {
          document.execCommand("fontname", false, "Microsoft YaHei");
          break;
        }
        case "SimSun": {
          document.execCommand("fontname", false, "SimSun");
          break;
        }
        case "KaiTi": {
          document.execCommand("fontname", false, "KaiTi");
          break;
        }
        case "YouYuan": {
          document.execCommand("fontname", false, "YouYuan");
          break;
        }
      }
    },
    //修改字体大小
    selectFontSize(newVal) {
      switch (newVal) {
        case "1": {
          document.execCommand("fontsize", false, "1");
          break;
        }
        case "2": {
          document.execCommand("fontsize", false, "2");
          break;
        }
        case "3": {
          document.execCommand("fontsize", false, "3");
          break;
        }
        case "4": {
          document.execCommand("fontsize", false, "4");
          break;
        }
        case "5": {
          document.execCommand("fontsize", false, "5");
          break;
        }
        case "6": {
          document.execCommand("fontsize", false, "6");
          break;
        }
        case "7": {
          document.execCommand("fontsize", false, "7");
          break;
        }
      }
    },
    //文本或标题
    selectHead(newVal) {
      switch (newVal) {
        case "h1": {
          document.execCommand("formatBlock", false, "<h1>");
          break;
        }
        case "h2": {
          document.execCommand("formatBlock", false, "<h2>");
          break;
        }
        case "h3": {
          document.execCommand("formatBlock", false, "<h3>");
          break;
        }
        case "h4": {
          document.execCommand("formatBlock", false, "<h4>");
          break;
        }
        case "h5": {
          document.execCommand("formatBlock", false, "<h5>");
          break;
        }
        case "h6": {
          document.execCommand("formatBlock", false, "<h6>");
          break;
        }
        case "h1": {
          document.execCommand("formatBlock", false, "<h7>");
          break;
        }
        case "p": {
          console.log(newVal);
          document.execCommand("formatBlock", false, "p");
          break;
        }
      }
    }
  },
  methods: {
    //撤销
    textUndo() {
      document.execCommand("undo", false, null);
    },
    //取消撤销
    textRedo() {
      document.execCommand("redo", false, null);
    },
    //加粗
    textStrong() {
      document.execCommand("bold", false, null);
    },
    //下划线
    textUnderline() {
      document.execCommand("underline", false, null);
    },
    //斜体
    textItalic() {
      document.execCommand("italic", false, null);
    },
    //居中对齐
    textJustifycenter() {
      document.execCommand("justifycenter", false, null);
    },
    //左对齐
    textJustifyleft() {
      document.execCommand("justifyleft", false, null);
    },
    //右对齐
    textJustifyright() {
      document.execCommand("justifyright", false, null);
    },
    //有序列表
    textOrderList() {
      document.execCommand("insertOrderedList", false, "<h1>");
    },
    //无序列表
    textUnorderList() {
      document.execCommand("insertUnorderedList", false, null);
    },
    //缩进
    textIndent() {
      document.execCommand("indent", false, null);
    },
    //取消缩进
    textOutdent() {
      document.execCommand("outdent", false, null);
    },
    //更改颜色
    //显示更改颜色菜单
    showChangeColorMenu() {
      this.isChangeColorMenu = !this.isChangeColorMenu;
      this.isChangeBackgroundColorMenu = false;
    },
    //点击颜色块后修改 字体颜色、颜色图标的颜色
    textChangeClor(val) {
      //参数： 'change-color-red'
      switch (val) {
        case "change-color-red": {
          //   this.iconFontColor = 'color:#ff0000';
          document.execCommand("foreColor", null, "#ff0000");
          //   this.isChangeColorMenu = !this.isChangeColorMenu;
          break;
        }
        case "change-color-yellow": {
          //   this.iconFontColor = 'color:yellow';
          document.execCommand("foreColor", null, "#ffff00");
          //   this.isChangeColorMenu = !this.isChangeColorMenu;
          break;
        }
        case "change-color-green": {
          //   this.iconFontColor = 'color:green';
          document.execCommand("foreColor", null, "#008000");
          //   this.isChangeColorMenu = !this.isChangeColorMenu;
          break;
        }
        case "change-color-black": {
          //   this.iconFontColor = 'color:black';
          document.execCommand("foreColor", null, "#000000");
          //   this.isChangeColorMenu = !this.isChangeColorMenu;
          break;
        }
        case "change-color-blue": {
          //   this.iconFontColor = 'color:#0000ff';
          document.execCommand("forecolor", false, "#0000ff");
          //   this.isChangeColorMenu = !this.isChangeColorMenu;
          break;
        }
      }
    },

    //显示背景颜色菜单
    showChangeBackgroundColorMenu() {
      this.isChangeBackgroundColorMenu = !this.isChangeBackgroundColorMenu;
      this.isChangeColorMenu = false;
    },

    //修改文字背景颜色
    textChangeBackgroundClor(val) {
      switch (val) {
        case "change-color-skyblue": {
          let select = document.getSelection();
          let selRange = select.getRangeAt(0);
          let span = document.createElement("span");
          span.style.backgroundColor = "skyblue";
          selRange.surroundContents(span);
          break;
        }
        case "change-color-yellow": {
          let select = document.getSelection();
          let selRange = select.getRangeAt(0);
          let span = document.createElement("span");
          span.style.backgroundColor = "yellow";
          selRange.surroundContents(span);
          break;
        }
        case "change-color-white": {
          let select = document.getSelection();
          let selRange = select.getRangeAt(0);
          let span = document.createElement("span");
          span.style.backgroundColor = "white";
          selRange.surroundContents(span);
          break;
        }
      }
    },

    //清除格式
    textRemoveAll() {
      document.execCommand("removeFormat", false, null);
    },

    //显示表情菜单
    showEmotionMenu() {
      this.isShowEmotionMunu = !this.isShowEmotionMunu;
    },

    //插入表情
    textEmotion(item) {
      document.execCommand("insertImage", false, item);
    },

    //全屏
    textFullScreen() {
      let fullscr = document.querySelector("html");
      if (!document.fullscreenElement) {
        this.fullScreen = "icon-shrink";
        fullscr.requestFullscreen();
      } else { 
        this.fullScreen = "icon-enlarge";
        document.mozCancelFullScreen(); 
      }
      //细节：解决按esc屏幕图标不会变化问题
      window.addEventListener('fullscreenchange',event =>{
        if(!document.fullscreenElement){//如果处于非全屏状态，图标显示放大
          this.fullScreen = "icon-enlarge";
        }
      })

    }
  }
};
</script>

<style>
.edit-container {
  position: relative;
  top: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  box-sizing: border-box;
}
.edit-div {
  box-sizing: border-box;
  display: flex;
  justify-content: flex-start;
  width: 800px;
  background: #f6f6f6;
  border-radius: 5px;
}
.edit-main {
  box-sizing: border-box;
  border: darkgray solid 1px;
  width: 800px;
  min-height: 300px;
  padding: 10px;
  border-radius: 5px;
}

.edit-main img {
  width: 25px;
  height: 25px;
  vertical-align: top;
}

.default-font {
  font-family: "YaHei";
  font-size: 16px;
}
</style>