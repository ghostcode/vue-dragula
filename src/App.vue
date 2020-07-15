<template>
  <div id="app">
    <h1><a href='https://github.com/bevacqua/dragula'><img src='./assets/logo.svg' alt='dragula'/></a></h1>
    <h3 class='tagline'><span class='tagline-text'>Drag and drop so simple it hurts</span></h3>
    <a href='https://github.com/bevacqua/dragula'>
      <img class='gh-fork' src='https://camo.githubusercontent.com/52760788cde945287fbb584134c4cbc2bc36f904/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f72696768745f77686974655f6666666666662e706e67' alt='Fork me on GitHub' data-canonical-src='https://s3.amazonaws.com/github/ribbons/forkme_right_white_ffffff.png' />
    </a>

    <div class='examples'>
      <div class='parent'>
        <label for='hy'>Move stuff between these two containers. Note how the stuff gets inserted near the mouse pointer? Great stuff.</label>
        <div class='wrapper'>
          <drag :options=options>
            <div id='left-defaults' class='container'>
              <div>You can move these elements between these two containers</div>
              <div>Moving them anywhere else isn't quite possible</div>
              <div>Anything can be moved around. That includes images, <a href='https://github.com/bevacqua/dragula'>links</a>, or any other nested elements.
              <div class='image-thing'><img src='./assets/icon.svg' onerror='this.src="resources/icon.png"' alt='dragula'/></div><sub>(You can still click on links, as usual!)</sub>
              </div>
            </div>
            <div id='right-defaults' class='container'>
              <div>There's also the possibility of moving elements around in the same container, changing their position</div>
              <div>This is the default use case. You only need to specify the containers you want to use</div>
              <div>More interactive use cases lie ahead</div>
              <div>Moving <code>&lt;input/&gt;</code> elements works just fine. You can still focus them, too. <input placeholder='See?' /></div>
              <div>Make sure to check out the <a href='https://github.com/bevacqua/dragula#readme'>documentation on GitHub!</a></div>
            </div>
          </drag>
        </div>
        <pre>
          <code v-pre>
            <drag>
              <div id="left">
                <p>1</p>
                <p>2</p>
                <p>3</p>
              </div>
              <div id="right">
                <p>1</p>
                <p>2</p>
                <p>3</p>
              </div>
            </drag>
          </code>
        </pre>
      </div>
    </div>   

    <div class='parent'>
      <label for='hy'>There are plenty of events along the lifetime of a drag event. Check out <a href='https://github.com/bevacqua/dragula#drakeon-events'>all of them</a> in the docs!</label>
      <div class='wrapper'>
        <div id='left-events' class='container'>
          <div>As soon as you start dragging an element, a <code>drag</code> event is fired</div>
          <div>Whenever an element is cloned because <code>copy: true</code>, a <code>cloned</code> event fires</div>
          <div>The <code>shadow</code> event fires whenever the placeholder showing where an element would be dropped is moved to a different container or position</div>
          <div>A <code>drop</code> event is fired whenever an element is dropped anywhere other than its origin <em>(where it was initially dragged from)</em></div>
        </div>
        <div id='right-events' class='container'>
          <div>If the element gets removed from the DOM as a result of dropping outside of any containers, a <code>remove</code> event gets fired</div>
          <div>A <code>cancel</code> event is fired when an element would be dropped onto an invalid target, but retains its original placement instead</div>
          <div>The <code>over</code> event fires when you drag something over a container, and <code>out</code> fires when you drag it away from the container</div>
          <div>Lastly, a <code>dragend</code> event is fired whenever a drag operation ends, regardless of whether it ends in a cancellation, removal, or drop</div>
        </div>
      </div>
      <pre>
        <code>
          dragula([document.getElementById(left), document.getElementById(right)])
            .on('drag', function (el) {
              el.className = el.className.replace('ex-moved', '');
            }).on('drop', function (el) {
              el.className += ' ex-moved';
            }).on('over', function (el, container) {
              container.className += ' ex-over';
            }).on('out', function (el, container) {
              container.className = container.className.replace('ex-over', '');
            });
        </code>
      </pre>
    </div>
    
  </div>
</template>

<script>
import Drag from '../vue-dragula.js'

export default {
  name: 'App',
  components: {
    Drag,
  },
  data() {
    return {
      options:{

      },
    }
  },
}
</script>

<style>

@import './app.css';

li{
  text-align: left;
}
.handle{
  cursor:move;
}

.gu-mirror {
  position: fixed !important;
  margin: 0 !important;
  z-index: 9999 !important;
  opacity: 0.8;
  -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=80)";
  filter: alpha(opacity=80);
}
.gu-hide {
  display: none !important;
}
.gu-unselectable {
  -webkit-user-select: none !important;
  -moz-user-select: none !important;
  -ms-user-select: none !important;
  user-select: none !important;
}
.gu-transit {
  opacity: 0.2;
  -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=20)";
  filter: alpha(opacity=20);
}

</style>
