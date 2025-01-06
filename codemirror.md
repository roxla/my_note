
> CodeMirror-widget

CodeMirror-widget 是 CodeMirror 提供的一种特殊的扩展，它可以在 CodeMirror 编辑器中添加各种自定义的组件和部件，例如按钮、下拉列表、菜单等等。

CodeMirror-widget 具有以下特点：

*   可以自定义部件的样式和行为；
*   可以在部件内部嵌入 HTML 和其他 Vue 组件；
*   可以通过 JavaScript 代码来操纵和控制部件的行为。

在 CodeMirror 中，使用 `CodeMirror.addWidget` 方法可以添加一个 Widget，它有以下参数：

*   `pos`：表示 Widget 的位置，可以是一个 `CodeMirror.Pos` 对象，也可以是一个 `{line: number, ch: number}` 对象；
*   `node`：表示 Widget 的 DOM 节点，可以是一个 HTML 元素，也可以是一个包含 HTML 内容的字符串；
*   `options`：表示 Widget 的选项，可以设置 Widget 的大小、样式、行为等属性。

下面是一个示例代码，演示了如何使用 CodeMirror-widget 在编辑器中添加一个按钮，并且当用户点击按钮时，弹出一个提示框：

vue

```vue
<template>
  <div>
    <textarea ref="editor" v-model="value"></textarea>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import CodeMirror from 'codemirror';
import 'codemirror/lib/codemirror.css';
import 'codemirror/mode/javascript/javascript';

export default defineComponent({
  props: {
    value: {
      type: String,
      default: ''
    },
    options: {
      type: Object,
      default: () => ({})
    }
  },
  mounted() {
    const { editor } = this.$refs;
    this.codeMirror = CodeMirror.fromTextArea(editor, {
      mode: 'javascript',
      ...this.options
    });
    this.addCustomButton();
  },
  beforeUnmount() {
    this.codeMirror.toTextArea();
  },
  methods: {
    addCustomButton() {
      const { cm } = this.codeMirror;
      const button = document.createElement('button');
      button.textContent = 'Click Me';
      button.addEventListener('click', () => {
        alert('Hello World!');
      });
      cm.addWidget(
        CodeMirror.Pos(0, 0),
        button,
        { coverGutter: false, insertAt: 0 }
      );
    }
  }
});
</script>
```

在这个示例中，我们通过 `CodeMirror.addWidget` 方法添加了一个按钮，按钮的位置为 `(0, 0)`，也就是在编辑器的左上角。当用户点击按钮时，会弹出一个提示框，内容为 "Hello World!"。需要注意的是，我们在 `addCustomButton` 方法中调用 `cm.addWidget` 方法，其中 `cm` 是 `this.codeMirror.cm` 的简写，它表示 CodeMirror 实例的内部 API，可以通过它来操纵和控制编辑器的行为。在 `addWidget` 方法中，我们可以设置 Widget 的选项，例如 `coverGutter` 表示 Widget 是否覆盖编辑器的行号列，`insertAt` 表示 Widget 插入到编辑器中的位置。在这个示例中，我们将 `coverGutter` 设置为 `false`