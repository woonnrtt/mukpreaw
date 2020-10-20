<template>
  <div>
    <h1>เพิ่มรายวิชา</h1>
  <div class="box">
    <form v-on:submit.prevent="createBlog">
      <p>
        รหัสวิชา:
        <input type="text" v-model="blog.title" />
      </p>
      <p>
        ชื่อรายวิชา: <input type="text" v-model="blog.content" />
      </p>
      <p>
        <vue-ckeditor
          v-model.lazy="blog.content"
          :config="config"
          @blur="onBlur($event)"
          @focus="onFocus($event)"
        />
      </p>
      <p>
        อาจารย์ประจำรายวิชา:
        <input type="text" v-model="blog.category" />
      </p>
      <p>
      <p>
        <button type="submit">เพิ่มรายวิชา</button>
      </p>
    </form></div>
  </div>
</template>
<script>
import BlogsService from "@/services/BlogsService";
import VueCkeditor from "vue-ckeditor2";

export default {
  data() {
    return {
      blog: {
        title: "",
        thumbnail: "null",
        pictures: "null",
        content: "",
        category: "",
        status: "",
      },
      config: {
        toolbar: [
          ["Bold", "Italic", "Underline", "Strike", "Subscript", "Superscript"],
        ],
        height: 300,
      },
    };
  },
  methods: {
    async createBlog() {
      try {
        await BlogsService.post(this.blog);
        this.$router.push({
          name: "blogs",
        });
      } catch (err) {
        console.log(err);
      }
    },

    onBlur(editor) {
      console.log(editor);
    },
    onFocus(editor) {
      console.log(editor);
    },
    
  },
  components: {
    VueCkeditor,
  },

  created() {
    this.config.toolbar = [
      {
        name: "document",
        items: [
          "Source",
          "-",
          "Save",
          "NewPage",
          "Preview",
          "Print",
          "-",
          "Templates",
        ],
      },
      {
        name: "clipboard",
        items: [
          "Cut",
          "Copy",
          "Paste",
          "PasteText",
          "PasteFromWord",
          "-",
          "Undo",
          "Redo",
        ],
      },
      {
        name: "editing",
        items: ["Find", "Replace", "-", "SelectAll", "-", "Scayt"],
      },
      {
        name: "forms",
        items: [
          "Form",
          "Checkbox",
          "Radio",
          "TextField",
          "Textarea",
          "Select",
          "Button",
          "ImageButton",
          "HiddenField",
        ],
      },
      "/",
      {
        name: "basicstyles",
        items: [
          "Bold",
          "Italic",
          "Underline",
          "Strike",
          "Subscript",
          "Superscript",
          "-",
          "CopyFormatting",
          "RemoveFormat",
        ],
      },
      {
        name: "paragraph",
        items: [
          "NumberedList",
          "BulletedList",
          "-",
          "Outdent",
          "Indent",
          "-",
          "Blockquote",
          "CreateDiv",
          "-",
          "JustifyLeft",
          "JustifyCenter",
          "JustifyRight",
          "JustifyBlock",
          "-",
          "BidiLtr",
          "BidiRtl",
          "Language",
        ],
      },
      { name: "links", items: ["Link", "Unlink", "Anchor"] },
      {
        name: "insert",
        items: [
          "Image",
          "Flash",
          "Table",
          "HorizontalRule",
          "Smiley",
          "SpecialChar",
          "PageBreak",
          "Iframe",
          "InsertPre",
        ],
      },
      "/",
      { name: "styles", items: ["Styles", "Format", "Font", "FontSize"] },
      { name: "colors", items: ["TextColor", "BGColor"] },
      { name: "tools", items: ["Maximize", "ShowBlocks"] },
      { name: "about", items: ["About"] },
    ];
  },
};
</script>
<style scoped>
</style>

<script>
import BlogsService from '@/services/BlogsService'
export default {
data () {
return {
blog: {
title: '',
thumbnail: 'null',
pictures: 'null',
content: '',
category: '',
status: 'saved'
}
}
},
methods: {
async createBlog () {
try {
await BlogsService.post(this.blog)
this.$router.push({
name: 'blogs'
})
} catch (err) {
console.log(err)
}
}
}
}
</script>
<style >
p{
  color: rgb(255, 255, 255);
}
  .box{
    background-color: rgb(226, 154, 67);
    margin: 5px;
    padding-left: 10px;
    padding: 10px;
}
</style>