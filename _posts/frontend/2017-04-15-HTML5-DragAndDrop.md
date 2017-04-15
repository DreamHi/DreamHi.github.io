---
layout: post
title: HTML5 Drag和Drop
categories: frontend
catalog: true
original: true
tags: HTML5 拖放
---

用鼠标选中一个元素进行移动就是简单的拖动。以往都需要利用第三方实现。
还好，现在成了HTML5标准的一部分，主流的浏览器都已支持。

任何元素都可以拖放，但是默认是不能拖动的。只需要给元素追加一个属性，就可以让其可拖动。

```html
<img draggable="true" />
```

### 拖动的过程

拖动开始(ondragstart) -> 设置拖动数据(setData) -> 放入位置(ondragover) -> 放置(ondrop)

dragstart -> drag -> dragenter -> dragover ->  dragleave  -> drop -> dragend

ondragover 事件规定在何处放置被拖动的数据。
默认地，无法将数据/元素放置到其他元素中。如果需要设置允许放置，我们必须阻止对元素的默认处理方式。

在拖动目标上触发的事件（源元素）：
* ondragstart:用户开始拖动元素时触发
* ondrag:元素正在拖动时触发
* ondragend:用户完成元素拖动后触发

释放目标时触发的事件
* ondragenter:当被鼠标拖动的对象进入其容器范围内时触发此事件
* ondragover:当某被拖动的对象在另一对象容器范围内拖动时触发此事件
* ondragleave:当被鼠标拖动的对象离开其容器范围内时触发此事件
* ondrop:在一个拖动过程中，释放鼠标键时触发此事件

### 简单例子

```html
<!DOCTYPE HTML>
<html>
   <head>

      <style type="text/css">
         #boxA, #boxB {
            float:left;padding:10px;margin:10px;-moz-user-select:none;
         }

         #boxA { background-color: #6633FF; width:75px; height:75px;  }
         #boxB { background-color: #FF6699; width:150px; height:150px; }
      </style>

      <script type="text/javascript">
         function dragStart(ev) {
            ev.dataTransfer.effectAllowed='move';
            ev.dataTransfer.setData("Text", ev.target.getAttribute('id'));
            ev.dataTransfer.setDragImage(ev.target,0,0);

            return true;
         }

         function dragEnter(ev) {
            event.preventDefault();
            return true;
         }

         function dragOver(ev) {
            return false;
         }

         function dragDrop(ev) {
            var src = ev.dataTransfer.getData("Text");
            ev.target.appendChild(document.getElementById(src));
            ev.stopPropagation();
            return false;
         }
      </script>

   </head>
   <body>

      <center>
         <h2>Drag and drop HTML5 demo</h2>
         <div>Try to move the purple box into the pink box.</div>

         <div id="boxA" draggable="true"
            ondragstart="return dragStart(ev)">
            <p>Drag Me</p>
         </div>

         <div id="boxB" ondragenter="return dragEnter(ev)"
            ondrop="return dragDrop(ev)"
            ondragover="return dragOver(ev)">Dustbin
         </div>

      </center>

   </body>
</html>
```

### 第三方库
* [dragula](https://bevacqua.github.io/dragula/)
* [Sortable](http://rubaxa.github.io/Sortable/)
* [Drag and Drop for React](http://react-dnd.github.io/react-dnd/)
* [react-grid-layout](https://github.com/STRML/react-grid-layout)